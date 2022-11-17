# User Holidays

German: "Urlaubsanspruch"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /users/holidays](#get-usersholidays)
- [GET /users/holidays/{id}](#get-usersholidaysid)
- [POST /users/holidays](#post-usersholidays)
- [PUT /users/holidays/{id}](#put-usersholidaysid)
- [DELETE /users/holidays/{id}](#delete-usersholidaysid)

<!-- /TOC -->

## Attributes

Holidays contain among the standard fields also:

- User (creator)

```json
{
  "id": 12345,
  "year": 2019,
  "title": "Urlaubsanspruch 80%",
  "days": 20,
  "hours": 160,
  "user": {
    "id": 933590696,
    "firstname": "John",
    "lastname": "Doe"
  },
  "creator": {
    "id": 933590697,
    "firstname": "Jane",
    "lastname": "Doe"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

Holiday credits have to be set in days. Holiday days are also converted to hours using the _daily hours_ value that may
be set for every user in the holiday section in MOCO: 10 days at 5h/day = 50 hours and 10 days at 8h/day = 80 hours.

## GET /users/holidays

Retrieve all holidays:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/holidays?year=2018' \
  -H 'Authorization: Token token=YOUR_API_KEY'
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
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /users/holidays

Create a holiday:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/users/holidays' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "user_id": 933590696,
        "year": 2019,
        "title": "Urlaubsanspruch 80%",
        "days": 20,
      }'
```

Mandatory fields are marked with a star (\*):

- **year\*** – 2019
- **title\*** – "Urlaubsanspruch 80%"
- **days\*** – 20
- **user_id\*** – 933590696
- **creator_id** – 933590000

## PUT /users/holidays/{id}

Update a holiday.

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/users/holidays/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "days": 22
      }'
```

All fields are analogous to the POST request.

## DELETE /users/holidays/{id}

Delete a holiday.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/users/holidays/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
