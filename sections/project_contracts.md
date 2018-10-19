# Project Contracts
German: "Projekte / Personal"

## Attributes

Assigning staff to a project is defined in Moco as a "contract".

```json
{       
    "id": 760253573,
    "user_id": 938487474,
    "firstname": "Nicola",
    "lastname": "Piccinini",
    "billable": true,
    "active": true,
    "budget": 9900,
    "hourly_rate": 110
}
```

## GET /projects/{id}/contracts

Retrieve all staff assignments for a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/contracts' \
  -H 'Authorization: Token token={api-key}'
```

This returns an array with assignment information (see Attributes).

## GET /projects/{id}/contracts/{id}

Retrieve a single staff assignment on a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/contracts/{id}' \
  -H 'Authorization: Token token={api-key}'
```

## POST /projects/{id}/contracts

Assign a person to a project:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/contracts' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "user_id": 123456,
        "budget": 9900
      }'
```

Mandatory fields are marked with a star (*):

* **user_id*** – 123456
* **billable** – true/false
* **active** – true/false
* **budget** – 9900
* **hourly_rate** – 120

## PUT /projects/{id}/contracts/{id}

Update a staff assignment to a project:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/contracts/{id}' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "budget": 8800
      }'
```

Fields are analogous to the POST request (except `user_id`).

## DELETE /projects/{id}/contracts/{id}

⚠ Deleting a staff assignment on a project is only possible as long as no hours are tracked from this person.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/contracts/{id}' \
  -H 'Authorization: Token token={api-key}'
```
