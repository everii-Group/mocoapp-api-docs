---
layout: default
parent: Projects
grand_parent: Entities
---

# Project Group

German: "Projektgruppen"

- TOC
{:toc}

## Attributes

The project group representation contains, among the standard fields, also:

- projects
- company
- user

```json
{
  "id": 234,
  "name": "Project Group Name",
  "user": {
    "id": 933613686,
    "firstname": "Jane",
    "lastname": "Doe"
  },
  "company": {
    "id": 760553185,
    "name": "Acme Inc."
  },
  "budget": 42000.0,
  "currency": "EUR",
  "info": "An info text",
  "custom_properties": {},
  "customer_report_url": "https://mycompany.mocoapp.com/project_groups/961779869/customer_report/1142853e926ee7c4dd7e",
  "projects": [
    {
      "id": 944958556,
      "identifier": "P1234",
      "name": "Project Name",
      "active": true,
      "budget": 10000.0
    }
  ],
  "created_at": "2024-08-16T08:36:44Z",
  "updated_at": "2024-08-16T08:36:44Z"
}
```

## GET /projects/groups

Retrieve all projects:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/groups' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete project group information (see Attributes).

The following parameters can be supplied:

- [Global filters apply](../entities#global-filters)
- **user_id** – 123456
- **company_id** – 123456

## GET /projects/groups/{id}

Retrieve a single project group:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/groups/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns a single project group representation.
