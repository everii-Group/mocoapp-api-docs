# Project Payment Schedules

German: "Projekte / Geplante Abrechnungen"

## Attributes

Payment schedules for fixed price projects.

```json
{
  "id": 760153573,
  "date": "2017-04-05",
  "net_total": 1000,
  "project": {
    "id": 822322322,
    "identifier": "P0077",
    "name": "New website"
  },
  "checked": false,
  "billed": false,
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /projects/{project_id}/payment_schedules

Retrieve all payment schedules for the project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{project_id}/payment_schedules' \
  -H 'Authorization: Token token={api-key}'
```

## GET /projects/{project_id}/payment_schedules/{id}

Retrieve a single payment schedule on a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{project_id}/payment_schedules/{id}' \
  -H 'Authorization: Token token={api-key}'
```

## POST /projects/{project_id}/payment_schedules

Create a paymennt schedule for the project:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{project_id}/payment_schedules' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
     	"net_total": 1800,
	    "date": "2019-10-28"
      }'
```

Mandatory fields are marked with a star (\*):

- **net_total\*** – 12000
- **date\*** – "2019-10-28"
- **checked** – true/false

## PUT /projects/{project_id}/payment_schedules/{id}

Update a payment schedule for a project:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{project_id}/payment_schedules/{id}' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "checked": true
      }'
```

Fields are analogous to the POST request.

## DELETE /projects/{project_id}/payment_schedules/{id}

⚠ Delete the payment schedule.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/projects/{project_id}/payment_schedules/{id}' \
  -H 'Authorization: Token token={api-key}'
```
