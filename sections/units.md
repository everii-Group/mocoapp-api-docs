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
