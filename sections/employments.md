---
layout: default
parent: Entities
---

# User Employments

German: "Wochenmodell"

- TOC
{:toc}

## Attributes

Employments contain among the standard fields also:

- User

```json
{
  "id": 982237015,
  "weekly_target_hours": 29.75,
  "pattern": {
    "am": [0, 4.25, 4.25, 4.25, 4.25],
    "pm": [0, 4.25, 4.25, 4.25, 0]
  },
  "from": "2017-01-01",
  "to": null,
  "user": {
    "id": 933590696,
    "firstname": "John",
    "lastname": "Doe"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /users/employments

Retrieve all employments:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/employments' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array of all employments.

The following parameters can be supplied:

- **from, to** – "2018-01-01", "2018-12-31" (`from` has to be provided, `to` can be left blank for all open ended employments)
- **user_id** – 123

## POST /users/employments

Create an employment:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/users/employments' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "user_id": 123,
        "pattern": {
          "am": [0, 4.25, 4.25, 4.25, 4.25],
          "pm": [0, 4.25, 4.25, 4.25, 0]
        },
        "from": "2022-01-01",
        "to": "2022-12-31",
      }'
```

Mandatory fields are marked with a star (\*):

- **user_id\*** – 123
- **pattern\*** – `{ "am": [4, 4, 4, 4, 4], "pm": [4, 4, 4, 4, 4] }` the work hours during morning and afternoon on each workday
- **from** – "2022-01-01" when the employment comes/came into effect (default: the current date)
- **to** – "2022-12-31" when the employment stops being in effect (default: unset)

## GET /users/employments/{id}

Retrieve a single employment:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/employments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## PUT /users/employments/{id}

Update an employment:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/users/employments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "pattern": {
          "am": [0, 4, 4, 4, 4],
          "pm": [0, 4, 4, 4, 4]
        }
      }'
```

Fields are analogous to the POST request but `user_id` and `pattern` are not mandatory.

## DELETE /users/employments/{id}

Delete an employment:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/users/employments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
