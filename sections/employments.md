# User Employments

German: "Wochenmodell"

## Attributes

Employments contain among the standard fields also:

- User

```json
{
  "id": 982237015,
  "weekly_target_hours": 29.75,
  "pattern": {
    "am": [0, 4.25, 4.25, 4.25, 4.25], // Mon - Fri
    "pm": [0, 4.25, 4.25, 4.25, 0] // Mon - Fri
  },
  "from": "2017-01-01",
  "to": null,
  "user": {
    "id": 933590696,
    "firstname": "John",
    "lastname": "Doe"
  },
  "created_at": "2018-10-17 09:33:46 UTC",
  "updated_at": "2018-10-17 09:33:46 UTC"
}
```

## GET /users/employments

Retrieve all employments:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/employments' \
  -H 'Authorization: Token token={api-key}'
```

This returns an array of all employments.

The following parameters can be supplied:

- **from, to** – "2018-01-01", "2018-12-31" (`from` has to be provided, `to` can be left blank for all open ended employments)
- **user_id** – 123

## GET /users/employments/{id}

Retrieve a single employment:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/employments/{id}' \
  -H 'Authorization: Token token={api-key}'
```
