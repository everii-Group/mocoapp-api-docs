---
layout: default
parent: Purchases
grand_parent: Entities
---

# Purchase Categories

{: .note }
This documentation is outdated, please refer to [our OpenAPI spec](https://docs.mocoapp.com/api/docs/v1#tag/purchasecategories).

German: "Ausgaben – Kategorien"

- TOC
{:toc}

## Attributes

The purchase category representation is:

```json
{
  "id": 123,
  "name": "Travel expenses",
  "credit_account": "6640",
  "active": true,
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /purchases/categories

Retrieve all categories:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases/categories' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete category information (see attributes).

The following parameters can be supplied:

- [Global filters apply](../entities#global-filters)

## GET /purchases/categories/{id}

Retrieve a single category:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases/categories/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

The response is a single category representation.
