{
"id": 8601,
"name": "Konfessionslos",
"name_en": "",
"placeholder": "",
"placeholder_en": "",
"entity": "User",
"kind": "Boolean",
"print_on_invoice": false,
"print_on_offer": false,
"print_on_timesheet": false,
"notification_enabled": false,
"defaults": [],
"updated_at": "2021-04-15T15:31:28Z",
"created_at": "2021-04-15T15:31:22Z"
}

# Custom Properties

German: "Eigene Felder"

<!-- TOC depthfrom:2 -->

- [Attributes](#attributes)
- [GET /account/custom_properties](#get-accountcustom_properties)

<!-- /TOC -->

## Attributes

- **entity** – any kind of entity that a custom property can be added to
- **kind** – String | Textarea | Link | Boolean | Select | MultiSelect | Date
- **defaults** – for selections: the options that can be selected, empty strings are also valid.
- **placeholder** – the placeholder text displayed on MOCO for input fields

```json
{
  "id": 8601,
  "name": "Purchase Ordner Number",
  "name_en": "Purchase Ordner Number",
  "placeholder": "",
  "placeholder_en": "",
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

- **entity** – Project (any kind of entity that a custom property can be added to)

returns:

```json
[
  {
    "id": 8601,
    "name": "Purchase Ordner Number",
    "name_en": "Purchase Ordner Number",
    "placeholder": "",
    "placeholder_en": "",
    "entity": "Project",
    "kind": "String",
    "print_on_invoice": true,
    "print_on_offer": false,
    "print_on_timesheet": true,
    "notification_enabled": false,
    "defaults": [],
    "updated_at": "2022-08-15T15:31:28Z",
    "created_at": "2022-08-15T15:31:22Z"
  },
  {
    "id": 6453,
    "name": "Hired via",
    "name_en": "Hired via",
    "placeholder": "",
    "placeholder_en": "",
    "entity": "User",
    "kind": "Select",
    "print_on_invoice": false,
    "print_on_offer": false,
    "print_on_timesheet": false,
    "notification_enabled": false,
    "defaults": ["Application", "Referral", "Other"],
    "updated_at": "2022-08-15T15:31:28Z",
    "created_at": "2022-08-15T15:31:22Z"
  }
]
```
