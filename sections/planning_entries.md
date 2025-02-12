---
layout: default
parent: Entities
---

# Planning Entries

German: "Planung"

- TOC
{:toc}

## Attributes

The planning entry representation contains among the standard fields also:

- assigned user (staff)
- *either* project *or* deal, the other is set to `null`
- deal attributes (project attributes are given in the example below):
  ```json
  {
    "id": 6542,
    "name": "Redesign website",
    "customer_name": "Acme GmbH",
    "color": "#aacb84"
  }
  ```


```json
{
  "id": 4839,
  "starts_on": "2020-05-04",
  "ends_on": "2020-05-04",
  "hours_per_day": 6.0,
  "comment": "",
  "symbol": null,
  "color": "#2965cc",
  "read_only": false,
  "user": {
    "id": 5484,
    "firstname": "Thomas",
    "lastname": "Munster"
  },
  "project": {
    "id": 4553,
    "identifier": "130",
    "name": "Support",
    "customer_name": "Acme GmbH",
    "color": "#faeb44"
  },
  "deal": null,
  "series_id": null,
  "tentative": false,
  "series_repeat": null,
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /planning_entries

Retrieve all planning entries (paged):

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/planning_entries?period=2020-04-01:2020-07-31' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete information about the planning entries (see Attributes).

The following parameters can be supplied:

- [Global filters apply](../entities#global-filters)
- **period** – "2020-05-01:2020-07-31"
- **user_id** – 123
- **project_id** – 345

## GET /planning_entries/{id}

Retrieve a single planning entry:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/planning_entries/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /planning_entries

Create a planning entry:

The entry is always created with the user that's executing the request (authorization token) if no `user_id` is supplied.

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/planning_entries' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "project_id": 4322,
        "starts_on": "2020-05-20",
        "ends_on": "2020-05-30",
        "hours_per_day": 3,
        "comment": "A comment...",
        "symbol": 2
      }'
```

Mandatory fields are marked with a star (\*):

- either **project_id\*** or **deal_id\*** – 4322 (project or deal ID)
- **starts_on\*** – "2020-05-20"
- **ends_on\*** – "2020-05-30"
- **hours_per_day\*** – 3
- **user_id** – 234567 (user ID for active staff)
- **comment** – "A comment..."
- **symbol** – 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 (home, building, car, graduation cap, cocktail, bells, baby carriage, users, moon , info circle)
- **tentative** - true / false (whether this is a blocker or not)

## PUT /planning_entries/{id}

Update a planning entry:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/planning_entries/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "hours_per_day": 5
      }'
```

Fields are analogous to the POST request.

## DELETE /planning_entries/{id}

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/planning_entries/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
