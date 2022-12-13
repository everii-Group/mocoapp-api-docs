---
layout: default
parent: Purchases
grand_parent: Entities
---

# Purchase Categories

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

- **ids** – e.g. `123,456` (IDS, comma-separated)
- **updated_after** - e.g. `2022-09-01T14:00:00Z` ISO8601 timestamp, only records that have been updated/created after

## GET /purchases/categories/{id}

Retrieve a single category:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases/categories/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

The response is a single category representation.
