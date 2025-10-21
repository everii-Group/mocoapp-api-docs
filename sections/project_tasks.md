---
layout: default
parent: Projects
grand_parent: Entities
---

# Project Tasks

German: "Projekte / Leistungen"

- TOC
{:toc}

## Attributes

```json
{
  "id": 760253573,
  "name": "Projektleitung",
  "billable": true,
  "active": true,
  "budget": 2900,
  "hourly_rate": 120,
  "revenue_category": {
    "id": 126,
    "name": "Projektleitung",
    "revenue_account": 30058,
    "cost_category": "PM1"
  },
  "description": "A task description",
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /projects/{id}/tasks

Retrieve all tasks on a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/tasks' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete task information (see Attributes).

## GET /projects/{id}/tasks/{id}

Retrieve a single task on a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/tasks/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /projects/{id}/tasks

Create a task on a project:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/tasks' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
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
- **description** – A description of this task

## PUT /projects/{id}/tasks/{id}

Update a task on a project:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/tasks/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "budget": 5000,
        "hourly_rate": 130
      }'
```

Fields are analogous to the POST request.

## DELETE /projects/{id}/tasks/{id}

{: .note }
Deleting a task on a project is only possible as long as no hours were tracked on this task.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/tasks/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## DELETE /projects/{id}/tasks/destroy_all

{: .warning }
Not deletable tasks on a project will be skipped.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/tasks/destroy_all' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
