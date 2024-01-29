---
layout: default
parent: Entities
has_children: true
---

# Users

German: "Personal"

- TOC
{:toc}

## Attributes

```json
{
  "id": 123,
  "firstname": "Max",
  "lastname": "Muster",
  "active": true,
  "extern": false,
  "email": "max.muster@beispiel.de",
  "mobile_phone": "+49 177 123 45 67",
  "work_phone": "+49 40 123 45 67",
  "home_address": "",
  "info": "",
  "birthday": "1970-01-01",
  "iban": "CH3181239000001245689",
  "avatar_url": "https//meinefirma.mocoapp.com/.../profil.jpg",
  "tags": ["Deutschland"],
  "custom_properties": {
    "Starting Month": "January 2015"
  },
  "unit": {
    "id": 456,
    "name": "Geschäftsleitung"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /users

Retrieve all staff:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete staff information (see Attributes).

The following parameters can be supplied:

- [Global filters apply](../entities#global-filters)
- **include_archived** – true/false (deactivated users)

## GET /users/{id}

Retrieve a single staff member:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns a single staff member representation.

## POST /users

Create a staff member:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/users' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "firstname": "Carmen",
        "lastname": "Sandiego",
        "email": "carmen.sandiego@acme.corp",
        "password": "dAfsdf88fw8fKjtD28f293!",
        "unit_id": 123
      }'
```

Mandatory fields are marked with a star (\*):

- **firstname\*** – "Peter"
- **lastname\*** – "Müller"
- **email\*** – "peter.mueller@meinefirma.de"
- **password\*** – "dAfsdf88fw8fKjtD28f293!"
- **unit_id\*** – 123 (team ID)
- **active** – true/false (activated/deactivated)
- **external** – true/false (external employee / contractor)
- **language** – "de", "de-AT", "de-CH", "en", "it" or "fr"
- **mobile_phone** – "+41 79 123 45 67"
- **work_phone** – "+41 44 123 45 67"
- **home_address** – "Peter Müller\nBeispielstrasse 123\nBeispielstadt"
- **bday** – "1975-01-17"
- **iban** - "CH3181239000001245689"
- **work_phone** – "+41 44 123 45 67"
- **tags** – ["Switzerland"]
- **custom_properties** – {"Starting Month": "01.01.2016"}
- **info** – "Info for this person..."

## PUT /users/{id}

Update a staff member:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/users/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "lastname": "Casanova",
        "email": "carmen.casanova@acme.corp",
      }'
```

Fields are analogous to the POST request. A related [employment](employments.md) must be termined separately.

## DELETE /users/{id}

{: .note }
Deleting a staff member is only possible if no hours are billed already.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/users/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## GET /users/{id}/performance_report

Retrieve a report on tracked hours vs target hours:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/{id}/performance_report' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns a performance report for this user:

```json
{
  "annually": {
    "year": 2021,
    "employment_hours": 1670.4,
    "target_hours": 1606.4,
    "hours_tracked_total": 210.95,
    "variation": -1395.45,
    "variation_until_today": -0.25,
    "hours_billable_total": 190.95
  },
  "monthly": [
    {
      "year": 2021,
      "month": 1,
      "target_hours": 128.0,
      "hours_tracked_total": 133.71,
      "variation": 5.71,
      "hours_billable_total": 113.95
    },
    {
      "year": 2021,
      "month": 2,
      "target_hours": 128.0,
      "hours_tracked_total": 77.24,
      "variation": -50.76,
      "hours_billable_total": 67.95
    },
    {
      "year": 2021,
      "month": 3,
      "target_hours": 115.2,
      "hours_tracked_total": 0.0,
      "variation": -115.2,
      "hours_billable_total": 0.0
    },
    {
      "year": 2021,
      "month": 4,
      "target_hours": 128.0,
      "hours_tracked_total": 0.0,
      "variation": -128.0,
      "hours_billable_total": 0.0
    },
    {
      "year": 2021,
      "month": 5,
      "target_hours": 121.6,
      "hours_tracked_total": 0.0,
      "variation": -121.6,
      "hours_billable_total": 0.0
    },
    {
      "year": 2021,
      "month": 6,
      "target_hours": 140.8,
      "hours_tracked_total": 0.0,
      "variation": -140.8,
      "hours_billable_total": 0.0
    },
    {
      "year": 2021,
      "month": 7,
      "target_hours": 140.8,
      "hours_tracked_total": 0.0,
      "variation": -140.8,
      "hours_billable_total": 0.0,
    },
    {
      "year": 2021,
      "month": 8,
      "target_hours": 140.8,
      "hours_tracked_total": 0.0,
      "variation": -140.8,
      "hours_billable_total": 0.0
    },
    {
      "year": 2021,
      "month": 9,
      "target_hours": 140.8,
      "hours_tracked_total": 0.0,
      "variation": -140.8,
      "hours_billable_total": 0.0
    },
    {
      "year": 2021,
      "month": 10,
      "target_hours": 134.4,
      "hours_tracked_total": 0.0,
      "variation": -134.4,
      "hours_billable_total": 0.0
    },
    {
      "year": 2021,
      "month": 11,
      "target_hours": 140.8,
      "hours_tracked_total": 0.0,
      "variation": -140.8,
      "hours_billable_total": 0.0
    },
    {
      "year": 2021,
      "month": 12,
      "target_hours": 147.2,
      "hours_tracked_total": 0.0,
      "variation": -147.2,
      "hours_billable_total": 0.0
    }
  ]
}
```

The following parameters can be supplied:

- **year** – e.g. 2021 (empty = current year)
