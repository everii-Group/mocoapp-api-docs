# User Presences
German: "Arbeitszeiten"

## Attributes

Presences contain among the standard fields also:
* User (creator)

```json
{
    "id": 982237015,
    "date": "2018-07-03",
    "from": "07:30",
    "to": "13:15",
    "user": {
        "id": 933590696,
        "firstname": "John",
        "lastname": "Doe"
    }
}
```

## GET /users/presences

Retrieve all presences:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/presences?from=2018-06-01&to=2018-06-30' \
  -H 'Authorization: Token token={api-key}'
```

This returns an array of all presences.

The following parameters can be supplied:

* **from, to** – "2018-06-01", "2018-06-30" (from and to have to be provided together)
* **user_id** – 123


## GET /users/presences/{id}

Retrieve a single presence:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/presences/{id}' \
  -H 'Authorization: Token token={api-key}'
```

## POST /users/presences

Create a presence:

Every presence is created for the user that the API key belongs to.

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/users/presences' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "date": "2017-06-11",
        "from": "08:00",
        "to": "10:00"
      }'
```

Mandatory fields are marked with a star (*):

* **date*** – "2017-06-11"
* **from*** – "08:00" (Start time, also: "0800" or "8")
* **to** – "12:30" (End time, can be left blank)

## PUT /users/presences/{id}

Update a presence.

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/users/presences/{id}' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "to": "14:00"
      }'
```

All fields are analogous to the POST request.

## DELETE /users/presences/{id}

Delete a presence.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/users/presences/{id}' \
  -H 'Authorization: Token token={api-key}'
```

