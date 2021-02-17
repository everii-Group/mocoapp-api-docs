# User Employments

German: "Wochenmodell"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /users/employments](#get-usersemployments)
- [GET /users/employments/{id}](#get-usersemploymentsid)

<!-- /TOC -->

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

## GET /users/employments/{id}

Retrieve a single employment:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/employments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
