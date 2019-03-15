# User Holidays

German: "Urlaub"

## Attributes

Holidays contain among the standard fields also:

- User (creator)

```json
{
  "id": 12345,
  "year": 2019,
  "title": "Urlaubsanspruch 80%",
  "hours": 160,
  "user": {
    "id": 933590696,
    "firstname": "John",
    "lastname": "Doe"
  }
}
```

## GET /users/holidays

Retrieve all holidays:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/holidays?year=2018' \
  -H 'Authorization: Token token={api-key}'
```

This returns an array of all holidays.

The following parameters can be supplied:

- **year** – 2018
- **user_id** – 123

## GET /users/holidays/{id}

Retrieve a single holiday:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/holidays/{id}' \
  -H 'Authorization: Token token={api-key}'
```

## POST /users/holidays

Create a holiday:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/users/holidays' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "user_id": 933590696,
        "year": 2019,
        "title": "Urlaubsanspruch 80%",
        "hours": 160,
      }'
```

Mandatory fields are marked with a star (\*):

- **year\*** – 2019
- **title\*** – "Urlaubsanspruch 80%"
- **hours** – 160
- **user_id** – 933590696

## PUT /users/holidays/{id}

Update a holiday.

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/users/holidays/{id}' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "hours": 175
      }'
```

All fields are analogous to the POST request.

## DELETE /users/holidays/{id}

Delete a holiday.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/users/holidays/{id}' \
  -H 'Authorization: Token token={api-key}'
```
