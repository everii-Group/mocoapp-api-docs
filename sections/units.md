# Units / Teams

German: "Teams"

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
      "lastname": "Miesel"
    },
    {
      "id": 933589599,
      "firstname": "Sabine",
      "lastname": "Schäuble"
    }
  ],
  "created_at": "2018-10-17 09:33:46 UTC",
  "updated_at": "2018-10-17 09:33:46 UTC"
}
```

## GET /units

Retrieve all teams:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/units' \
  -H 'Authorization: Token token={api-key}'
```

This returns an array with complete team information (see Attributes).

## GET /units/{id}

Retrieve a single team:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/units/{id}' \
  -H 'Authorization: Token token={api-key}'
```
