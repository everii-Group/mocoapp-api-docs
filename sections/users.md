# Users

German: "Personal"

## Attributes

```json
{
  "id": 123,
  "firstname": "Max",
  "lastname": "Muster",
  "active": true,
  "external": false,
  "email": "max.muster@beispiel.de",
  "mobile_phone": "+49 177 123 45 67",
  "work_phone": "+49 40 123 45 67",
  "home_address": "",
  "info": "",
  "birthday": "1970-01-01",
  "avatar_url": "https//meinefirma.mocoapp.com/.../profil.jpg",
  "custom_properties": {
    "Starting Month": "January 2015"
  },
  "unit": {
    "id": 456,
    "name": "Geschäftsleitung"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /users

Retrieve all staff:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users' \
  -H 'Authorization: Token token={api-key}'
```

This returns an array with complete staff information (see Attributes).

The following parameters can be supplied:

- **include_archived** – true/false (deactivated users)

## GET /users/{id}

Retrieve a single staff member:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/{id}' \
  -H 'Authorization: Token token={api-key}'
```

This returns a single staff member representation.

## POST /users

Create a staff member:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/users' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "firstname": "Carmen",
        "lastname": "Sandiego",
        "email": "carmen.sandiego@acme.corp",
        "password": "dAfsdf88fw8fKjtD28f293!",
        "unit_id": 123
      }'
```

Mandatory fields are marked with a star (\*):

- **firstname\*** – "Peter"
- **lastname\*** – "Müller"
- **email\*** – "peter.mueller@meinefirma.de"
- **password\*** – "dAfsdf88fw8fKjtD28f293!"
- **unit_id\*** – 123 (team ID)
- **active** – true/false (activated/deactivated)
- **external** – true/false (external employee / contractor)
- **language** – "de", "de-AT", "de-CH", "en", "it" or "fr"
- **mobile_phone** – "+41 79 123 45 67"
- **work_phone** – "+41 44 123 45 67"
- **home_address** – "Peter Müller\nBeispielstrasse 123\nBeispielstadt"
- **bday** – "1975-01-17"
- **work_phone** – "+41 44 123 45 67"
- **custom_properties** – {"Starting Month": "01.01.2016"}
- **info** – "Info for this person..."

## PUT /users/{id}

Update a staff member:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/users/{id}' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "lastname": "Casanova",
        "email": "carmen.casanova@acme.corp",
      }'
```

Fiels are analogous to the POST request. A related [employment](employments.md) must be termined separately.

## DELETE /users/{id}

⚠ Deleting a staff member is only possible if no hours are billed already.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/users/{id}' \
  -H 'Authorization: Token token={api-key}'
```
