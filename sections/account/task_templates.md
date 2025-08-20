---
layout: default
title: Task Templates
parent: Account
grand_parent: Entities
---

# Task Templates

German: "Standardleistungen"

- TOC
{:toc}

## Attributes

Item attributes:

- **name***
- **description**
- **revenue_category**
- **billable** true / false
- **project_default** true / false - adding to new projects by default
- **index** e.g. 10 - used for ordering

```json
{
  "id": 1,
  "name": "Service A",
  "description": "A description",
  "revenue_category": {
    "id": 4567,
    "name": "Revenue category name",
    "revenue_account": 1000,
    "cost_category": 99
  },
  "billable": true,
  "project_default": true,
  "index": 10,
  "created_at": "2025-07-17T18:14:31Z",
  "updated_at": "2022-08-18T08:17:55Z"
}
```

## GET /account/task_templates

Retrieve task templates:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/task_templates' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

returns an array of task templates.

The following parameters can be supplied:

- [Global filters apply](../../entities#global-filters)

## GET /account/task_templates/{id}

Retrieve an task template:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/task_templates/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

returns a single task template.

## POST /account/task_templates

Create an task template:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/account/task_templates' \
  -H 'Authorization: Token token=YOUR_API_KEY'
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Web Development",
        "description": "Building the web application",
        "revenue_category_id": 4567,
        "billable": true,
        "project_default": true
      }'
```

Mandatory fields are: name.

## PUT /account/task_templates/{id}

Update an task template:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/account/task_templates/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
  -H 'Content-Type: application/json' \
  -d '{
        "title": "Development"
      }'
```

## DELETE /account/task_templates/{id}

Delete an task template:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/account/task_templates/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
