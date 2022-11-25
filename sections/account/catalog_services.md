---
layout: default
title: Account / Catalog Services
parent: Entities
---

# Catalog Services

German: "Leistungskatalog"

- TOC
{:toc}

## Attributes

Item attributes:

- **type** `title` / `description` / `item` / `page-break` / `subtotal` / `separator` - position type
- **description** (`description` type only)
- **quantity** can be 0 for all-inclusive item (detailed `item` type only)
- **unit** only used for detailed `item` type, could be e.g. "hours" or "pieces", (detailed `item` type only)
- **unit_price** price for a single unit (detailed `item` type only)
- **net_total** total price for this position (`item` type only)
- **unit_cost** internal cost for 1 unit (`item` type only)
- **optional** optional position (`item` type only)
- **part** `subtotal` type only, part "true" means subtotal to the upper `title`, "false" means for the whole document
- **additional** mark as additional service

```json
{
  "id": 20370,
  "title": "Catalog entry",
  "items": [
    {
      "id": 113400,
      "type": "item",
      "title": "Setup",
      "description": null,
      "quantity": 0.0,
      "unit": null,
      "unit_price": 0.0,
      "net_total": 1200.0,
      "unit_cost": 0.0,
      "optional": false,
      "part": false,
      "additional": false,
      "created_at": "2022-06-16T12:24:30Z",
      "updated_at": "2022-06-16T12:24:30Z"
    },
    {
      "id": 76675,
      "type": "item",
      "title": "Consulting",
      "description": null,
      "quantity": 20.0,
      "unit": "h",
      "unit_price": 150.0,
      "net_total": 3000.0,
      "unit_cost": 0.0,
      "optional": false,
      "part": false,
      "additional": false,
      "created_at": "2022-06-16T12:24:30Z",
      "updated_at": "2022-06-16T12:24:30Z"
    }
  ],
  "created_at": "2022-06-16T12:24:30Z",
  "updated_at": "2022-06-16T12:24:30Z"
}
```

## GET /account/catalog_services

Retrieve catalog services:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/catalog_services' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

returns an array of catalog services including their items.

## GET /account/catalog_services/{id}

Retrieve catalog services:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/catalog_services/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

returns a single catalog service.

## POST /account/catalog_services

Create a catalog service including their items

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/account/catalog_services' \
  -H 'Authorization: Token token=YOUR_API_KEY'
  -H 'Content-Type: application/json' \
  -d '{
        "title": "Catalog entry",
        "items": [
          {
            "type": "item",
            "title": "Setup",
            "net_total": 1200.0
          },
          {
            "type": "item",
            "title": "Consulting",
            "quantity": 20.0,
            "unit": "h",
            "unit_price": 150.0,
            "net_total": 3000.0
          }
        ]
      }'
```

## PUT /account/catalog_services/{id}

Update a catalog service:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/account/catalog_services/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
  -H 'Content-Type: application/json' \
  -d '{
        "title": "Catalog entry"
      }'
```

The items cannot be updated this way, use the separate endpoints for this.

## DELETE /account/catalog_services/{id}

Delete a catalog service:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/account/catalog_services/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
  -H 'Content-Type: application/json' \
  -d '{
        "title": "Catalog entry"
      }'
```

## GET /account/catalog_services/{service_id}/items/{id}

Get an item within a service:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/catalog_services/{service_id}/items/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /account/catalog_services/{service_id}/items

Create a new item within a service:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/account/catalog_services/{service_id}/items' \
  -H 'Authorization: Token token=YOUR_API_KEY'
  -H 'Content-Type: application/json' \
  -d '{
        "type": "item",
        "title": "Consulting",
        "quantity": 20.0,
        "unit": "h",
        "unit_price": 150.0,
        "net_total": 3000.0
      }'
```

## PUT /account/catalog_services/{service_id}/items/{id}

Update an item:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/account/catalog_services/{service_id}/items/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
  -H 'Content-Type: application/json' \
  -d '{
        "type": "item",
        "title": "Consulting",
        "quantity": 20.0,
        "unit": "h",
        "unit_price": 150.0,
        "net_total": 3000.0
      }'
```

## DELETE /account/catalog_services/{service_id}/items/{id}

Delete an item:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/account/catalog_services/{service_id}/items/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
