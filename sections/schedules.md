---
layout: default
parent: Entities
---

# Schedules

German: "Absenz"

- TOC
{:toc}

## Attributes

Schedules are now used for absences only. Use [Planning Entries](planning_entries.md) for project schedules.

The schedule representation contains among the standard fields also:

- assignment (absence)
- assigned user (staff)

```json
{
  "id": 123,
  "date": "2017-06-14",
  "comment": "Half day off",
  "am": true,
  "pm": true,
  "symbol": null,
  "assignment": {
    "id": 789,
    "name": "Holiday",
    "code": "4",
    "customer_name": "hundertzehn GmbH",
    "color": "#BBB",
    "type": "Absence"
  },
  "user": {
    "id": 567,
    "firstname": "Sabine",
    "lastname": "Schäuble"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /schedules

Retrieve all absences (paged):

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/schedules?from=2018-10-01&to=2018-10-31' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete schedule information (see Attributes).

Additionally, the following parameters can be supplied:

- [Global filters apply](../entities#global-filters)
- **from** – "2017-05-01"
- **to** – "2017-05-31"
- **user_id** – 123
- **absence_code** – 1, 2, 3, 4, 5 (unplannable absence, public holiday, sick day, holiday, absence)

## GET /schedules/{id}

Retrieve a single planning entry:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/schedules/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /schedules

Create a planning entry:

The entry is always created with the user that's executing the request (authorization token) if no `user_id` is supplied.

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/schedules' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "date": "2018-10-01",
        "absence_code": "4"
      }'
```

Mandatory fields are marked with a star (\*):

- **date\*** – "2017-06-11"
- **absence_code\*** – 1, 2, 3, 4, 5 (unplannable absence, public holiday, sick day, holiday, absence)
- **user_id** – 234567 (user ID for active staff)
- **am** – true, false (morning yes/no)
- **pm** – true, false (afternoon yes/no)
- **comment** – "A comment..."
- **symbol** – 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 (home, building, car, graduation cap, cocktail, bells, baby carriage, users, moon, info circle, dot circle, exlamation mark)
- **overwrite** – true, false (override existing entry)

## PUT /schedules/{id}

Update a planning entry:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/schedules/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "comment": "A comment",
      }'
```

Fields are analogous to the POST request.

## DELETE /schedules/{id}

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/schedules/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
