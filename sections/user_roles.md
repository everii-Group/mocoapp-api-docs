---
layout: default
parent: Entities
---

# User permission roles

German: "Benutzerrollen"

- TOC
{:toc}

## Attributes

The representation contains among the standard fields also:

- permission (the permission granted with this role)

```json
{
  "id": 42,
  "name": "Entwickler",
  "is_default": false,
  "is_admin": false,
  "permission": {
    "report": "none",
    "companies": "full",
    "contacts": "full",
    "people": "none",
    "purchases": "none",
    "settings": "none",
    "sales": "none",
    "projects": "full",
    "calendar": "full",
    "time_tracking": "full",
    "invoicing": "none"
  },
  "created_at": "2024-10-17T09:33:46Z",
  "updated_at": "2024-10-17T09:33:46Z"
}
```

## GET /users/roles

Retrieve all the roles:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/users/roles' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete role information (see Attributes).
