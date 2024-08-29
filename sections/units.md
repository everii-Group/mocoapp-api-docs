---
layout: default
parent: Entities
---

# Units / Teams

German: "Teams"

- TOC
{:toc}

## Attributes

The representation contains among the standard fields also:

- users (staff assigned to this team)

```json
{
  "id": 909147861,
  "name": "C Office",
  "users": [
    {
      "id": 933590158,
      "firstname": "Tobias",
      "lastname": "Miesel",
      "email": "tobias@domain.com"
    },
    {
      "id": 933589599,
      "firstname": "Sabine",
      "lastname": "Schäuble",
      "email": "sabine@domain.com"
    }
  ],
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /units

Retrieve all teams:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/units' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete team information (see Attributes).

Additionally, the following parameters can be supplied:

- [Global filters apply](../entities#global-filters)

## GET /units/{id}

Retrieve a single team:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/units/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /units

Create a unit:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/units' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "A great new team"
      }'
```

{: .note }
Assigning a user is possible by [updating it](users.md#put-usersid) with the `unit_id` attribute.

## PUT /units/{id}

Update a unit:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/units/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "A new name"
      }'
```

Fields are analogous to the POST request.

## DELETE /users/{id}

{: .note }
Deleting a unit is only possible if no users are assigned to it. Move existing users to a different unit by [updating them](users.md#put-usersid) with the `unit_id` attribute.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/units/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```