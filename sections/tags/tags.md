---
layout: default
title: Tags (Labels)
parent: Tags (Labels)
grand_parent: Entities
---

# Tags

- TOC
{:toc}

## Attributes

```json
{
  "id": 12345678,
  "name": "Important",
  "color": "#FF0000",
  "context": "Project",
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /tags

Retrieve the list of tags:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/tags'
```

This returns an array of all tags.

The following parameters can be supplied:

- [Global filters apply](../entities#global-filters)
- **context** – one of Company, Contact, Project, Deal, Purchase, Invoice, Offer or User

## GET /tags/{id}

Retrieve a single tag:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/tags/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /tags

Create a tag:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/tags' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "ONHOLD",
        "color: "#FFFF00",
        "context": "Project"
      }'
```

This creates a yellow tag "ONHOLD" for the projects area.

Mandatory fields are marked with a star (\*):

- **name\*** – "ONHOLD"
- **context\*** – one of Company, Contact, Project, Deal, Purchase, Invoice, Offer or User 
- **color** – must be in hex format `#ABC123`; default is grey 

## PUT /tags/{id}

Change a tag:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/tags/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "color": "#FF0000"
      }'
```

Only `name` and `color` can be changed (not the context or area in MOCO).

## DELETE /tags/{id}

Selectively remove the tags associated to the entity:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/tags/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

{: .note }
Pass `merge_tag_id` if you want to replace all tagged entities with another tag. Useful to consolidate many tags into one.
