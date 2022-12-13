---
layout: default
parent: Users
grand_parent: Entities
---

# User Presences

German: "Arbeitszeiten"

- TOC
{:toc}

## Attributes

Presences contain among the standard fields also:

- User (creator)

```json
{
  "id": 982237015,
  "date": "2018-07-03",
  "from": "07:30",
  "to": "13:15",
  "is_home_office": true,
  "user": {
    "id": 933590696,
    "firstname": "John",
    "lastname": "Doe"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /users/presences

Retrieve all presences:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/presences?from=2018-06-01&to=2018-06-30' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array of all presences.

The following parameters can be supplied:

- **from, to** – "2018-06-01", "2018-06-30" (from and to have to be provided together)
- **user_id** – 123
- **is_home_office** – true/false

## GET /users/presences/{id}

Retrieve a single presence:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/presences/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /users/presences

Create a presence:

Every presence is created for the user that the API key belongs to.

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/users/presences' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "date": "2018-06-11",
        "from": "08:00",
        "to": "10:00"
      }'
```

Mandatory fields are marked with a star (\*):

- **date\*** – "2018-06-11"
- **from\*** – "08:00"
- **to** – "12:30" (End time, can be left blank)
- **is_home_office** – true/false (default: `false`, will set the whole day)

## POST /users/presences/touch

This request creates a new presence and returns it for the user with the corresponding API-Key starting from the current time or terminates an existing open presence at the current time. Can be used to implement a time clock system (e.g. RFID).

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/users/presences/touch' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

A first request at 9:30 AM creates a presence with `from="09:30"`, a second request at 11:30 AM sets `to="11:30"` of the previous presence.

{: .note }
> There are two special situations to take into consideration:
> 
> 1. If a presence is started and stopped by `touch` within the same minute, then it is discarded.
> 2. If a `touch` conflicts with an existing presence, then the request is refused and the server response code
   is `423 Locked`.

```bash
curl -X POST \
 'https://{domain}.mocoapp.com/api/v1/users/presences/touch' \
 -H 'Authorization: Token token=YOUR_API_KEY' \
 -H 'Content-Type: application/json' \
 -d '{
       "is_home_office": true,
     }'
```

Optional fields:

- **is_home_office** – true/false (default: `false`, will set the whole day)
- **override** – "2022-03-27 14:45"

To prevent time differences during delays between systems, the parameter `override` can be passed with the time of the event in the format `YYYY-MM-DD HH:MM`. It has to be in 24h format and is timezone agnostic which means that MOCO stores the hour and minute in local time.

## PUT /users/presences/{id}

Update a presence.

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/users/presences/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
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
  -H 'Authorization: Token token=YOUR_API_KEY'
```
