# Project Tasks

German: "Projekte / Leistungen"

## Attributes

```json
{
  "id": 760253573,
  "name": "Projektleitung",
  "billable": true,
  "active": true,
  "budget": 2900,
  "hourly_rate": 120,
  "created_at": "2018-10-17 09:33:46 UTC",
  "updated_at": "2018-10-17 09:33:46 UTC"
}
```

## GET /projects/{id}/tasks

Retrieve all tasks on a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/tasks' \
  -H 'Authorization: Token token={api-key}'
```

This returns an array with complete task information (see Attributes).

## GET /projects/{id}/tasks/{id}

Retrieve a single task on a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/tasks/{id}' \
  -H 'Authorization: Token token={api-key}'
```

## POST /projects/{id}/tasks

Create a task on a project:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/tasks' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Design / UX",
        "billable": true,
        "hourly_rate": 120
      }'
```

Mandatory fields are marked with a star (\*):

- **name\*** – "Design / UX"
- **billable** – true/false
- **active** – true/false
- **budget** – 5000
- **hourly_rate** – 120

## PUT /projects/{id}/tasks/{id}

Update a task on a project:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/tasks/{id}' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "budget": 5000,
        "hourly_rate": 130
      }'
```

Fields are analogous to the POST request.

## DELETE /projects/{id}/tasks/{id}

⚠ Deleting a task on a project is only possible as long as no hours were tracked on this task.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/tasks/{id}' \
  -H 'Authorization: Token token={api-key}'
```
