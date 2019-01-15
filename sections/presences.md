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
        "date": "2018-06-11",
        "from": "08:00",
        "to": "10:00"
      }'
```

Mandatory fields are marked with a star (*):

* **date*** – "2018-06-11"
* **from*** – "08:00"
* **to** – "12:30" (End time, can be left blank)


## POST /users/presences/touch

This request creates a new presence starting from the current time or terminates an existing
open presence at the current time. Can be used to implement a time clock system (e.g. RFID).

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/users/presences/touch' \
  -H 'Authorization: Token token={api-key}'
```

A first request at 9:30 AM creates a presence with `from="09:30"`, a second request at 11:30 AM sets `to="11:30"` of the previous presence.

⚡ There are two special situations to take into consideration:
1. If a presence is started and stopped by `touch` within the same minute, then it is discarded.
2. If a `touch` conflicts with an existing presence, then the request is refused and the server response code
is `423 Locked`.


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
