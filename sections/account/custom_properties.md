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

## POST /account/custom_properties

Create a new custom property:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/account/custom_properties' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Slogan",
        "kind": "String",
        "entity": "Deal"
      }'
```

Mandatory fields are marked with a star (\*):

- **name\*** – "Slogan" name of the custom property
- **kind\*** – String | Textarea | Link | Boolean | Select | MultiSelect | Date
- **entity\*** – Deal | Project | Customer | ...
- **placeholder** – placeholder text displayed on MOCO for the input fields
- **placeholder_alt** – paceholder in the alternative language
- **print_on_invoice** – true/false (if true, the custom property is printed on invoices)
- **print_on_offer** – true/false (if true, the custom property is printed on offers)
- **print_on_timesheet** – true/false (if true, the custom property is printed on timesheets)
- **notification_enabled** – true/false (for kind `Date` a notification is sent to a user, dependent on the entity)
- **api_only** – true/false (if true, the custom property is not displayed in the UI, but can be used via the API)
- **defaults** – for selections: the options that can be selected, empty strings are also valid.

## PATCH /account/custom_properties/{id}

Update a new custom property:

```bash

curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/account/custom_properties' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Slogan",
        "placeholder": "Enter your slogan here",
      }'
```

Fields are analogous to the POST request, but `kind` and `entity` cannot be changed.

## DELETE /account/custom_properties/{id}

Deletes the custom property:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/account/custom_properties/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
