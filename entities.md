---
layout: default
title: Entities
has_children: true
---

# Entities

## Global Filters

All list/index endpoints offer a common set of filters.

### Filter `ids`

Usage: `GET /api/v1/entities?ids=123,456`

Allows you to filter by comma-separated IDs and fetch multiple entities.

### Filter `updated_after`

Usage: `GET /api/v1/entities?updated_after=2022-04-20T09:17:58Z` (ISO8601 timestamp)

Enables you to give a timestamp for all entities that are created or updated after this timestamp, especially useful for synchronisation purposes.

Combine it with a [webhook subscription](webhooks) on DELETE for the entity to have a complete synchronisation.

### Filter by Custom Fields – `custom_properties`

Allows you to filter entities by one or more custom fields. The filter for the custom fields is passed via the query-parameter `custom_properties`. To query entities that contain the value "Automotive" in a custom field named "Sector", the query would need to be as follows:

`GET /api/v1/entities?custom_properties[Sector]=Automotive`

{: .note }
Filtering by an unknown custom field will result in an empty result set!

#### Custom Fields of type MultiSelect

For custom fields of type `MultiSelect` can store multiple values. They can be queried by a single value or multiple values. Assuming there is a custom field named "Sector" of type `MultiSelect`, the following queries are possible:

- querying for a single value: `GET /api/v1/entities?custom_properties[Sector]=Pharma`

This will find entities with the value "Pharma" in the custom field named `Sector`. Additional values may be present in the custom field named "Sector" and the entity is still matched.

- querying for multiple values: `GET /api/v1/entities?custom_properties[Sector][]=Pharma&custom_properties[Sector][]=Chemistry`

This will find entities with both the values "Pharma" and "Chemistry" in the custom field named "Sector". Additional values may be present in the custom field named "Sector" and the entity is still matched.

The multiple values are given in the array bracket format (notice the empty bracket after the custom field name), i.e. `custom_properties[Sector][]=Pharma&custom_properties[Sector][]=Chemistry` will correspond to the following JSON:

```JSON
{ 
  "custom_properties": {
    "Sector": ["Pharma", "Chemistry"]
  }
}
```

While this `custom_properties[Sector]=Pharma` will correspond to the following JSON:

```JSON
{ 
  "custom_properties": {
    "Sector": "Pharma"
  }
}
```

Both are valid for querying custom field of type `MultiSelect`.

#### Custom Fields of type Boolean

Custom fields of type `Boolean` can be queried with `true` or `false`. Assuming there is a custom field named "Newsletter" of type `Boolean`, the following queries are possible:

-  `GET /api/v1/entities?custom_properties[Newsletter]=true`

Will find all entities for which the custom field named "Newsletter" is set to true.

-  `GET /api/v1/entities?custom_properties[Newsletter]=false`

Will find all entities for which the custom field named "Newsletter" is set to false.

{: .note }
This will not find entities for which the custom field named "Newsletter" was not set to any value.

#### Custom Fields of other types

Custom fields of type `Date` need to be queried with the date-format `YYYY-MM-DD`, e.g. query all entities with a "Subscription Date" of March 25th, 2024:

-  `GET /api/v1/entities?custom_properties[Subscription Date]=2024-03-25`

For custom fields of type `Select`, `Textarea`, `String`, `Link`, the queried value needs to match exactly, i.e. partial matches do not result in a match.
