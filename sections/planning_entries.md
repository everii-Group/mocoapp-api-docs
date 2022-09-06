# Planning Entries

German: "Planung"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /planning_entries](#get-planning_entries)
- [GET /planning_entry/{id}](#get-planning_entryid)
- [POST /planning_entry](#post-planning_entry)
- [PUT /planning_entries/{id}](#put-planning_entriesid)
- [DELETE /planning_entries/{id}](#delete-planning_entriesid)

<!-- /TOC -->

## Attributes

The planning entry representation contains among the standard fields also:

- assigned user (staff)
- project

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
    "customer_name": "Acme GmbH"
  },
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

- **ids** – e.g. `123,456` (IDS, comma-separated)
- **period** – "2020-05-01:2020-07-31"
- **user_id** – 123
- **project_id** – 345

## GET /planning_entry/{id}

Retrieve a single planning entry:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/planning_entries/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /planning_entry

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

- **project_id\*** – 4322 (project ID for active project)
- **starts_on\*** – "2020-05-20"
- **ends_on\*** – "2020-05-30"
- **hours_per_day\*** – 3
- **user_id** – 234567 (user ID for active staff)
- **comment** – "A comment..."
- **symbol** – 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 (home, building, car, graduation cap, cocktail, bells, baby carriage, users, moon , info circle)

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
