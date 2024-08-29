---
layout: default
parent: Purchases
grand_parent: Entities
---

# Purchase Budgets

German: "Ausgaben – Budgets"

- TOC
{:toc}

## Attributes

The purchase budget representation is:

```json
{
    "id": "2",
    "year": 2024,
    "title": "Betrieb – Hosting",
    "active": true,
    "target": 84000,
    "exhaused": 66483,
    "planned": 4494,
    "remaining": 13023
}
```

## GET /purchases/budget

Retrieve budgets for given year:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases/budgets?year=2023' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete budget information (see attributes).

The following parameters can be supplied:
- **year** – 2023

