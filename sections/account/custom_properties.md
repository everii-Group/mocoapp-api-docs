---
layout: default
title: Custom Properties
parent: Account
grand_parent: Entities
---

# Custom Properties

German: "Eigene Felder"

- TOC
{:toc}

## Attributes

- **entity** – any kind of entity that a custom property can be added to
- **kind** – `String` / `Textarea` / `Link` / `Boolean` / `Select` / `MultiSelect` / `Date`
- **defaults** – for selections: the options that can be selected, empty strings are also valid.
- **placeholder** – the placeholder text displayed on MOCO for input fields
- **notification_enabled** – for kind `Date` a notification is sent to a user (dependent on the entity).

```json
{
  "id": 8601,
  "name": "Purchase Order Number",
  "name_alt": "Numero Identificativo Acquisto",
  "placeholder": "",
  "placeholder_alt": "",
  "entity": "Project",
  "kind": "String",
  "print_on_invoice": true,
  "print_on_offer": false,
  "print_on_timesheet": true,
  "notification_enabled": false,
  "defaults": [],
  "updated_at": "2022-08-15T15:31:28Z",
  "created_at": "2022-08-15T15:31:22Z"
}
```

## GET /account/custom_properties

Retrieve custom properties:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/custom_properties' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

The following parameters can be supplied:

- [Global filters apply](../../entities#global-filters)
- **entity** – e.g. `Project` (any kind of entity that a custom property can be added to)

returns an array of custom properties.

## GET /account/custom_properties/{id}

Retrieve custom properties:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/custom_properties/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

returns a single custom property.
