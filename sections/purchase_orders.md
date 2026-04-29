---
layout: default
parent: Entities
has_children: true
---

# Purchase Orders

German: "Bestellungen"

Purchase orders define budgets for recurring or one-time purchases with a specific supplier, cost center, and user.

- TOC
{:toc}

## Attributes

The purchase order representation contains:

```json
{
  "id": 12345,
  "date": "2024-01-01",
  "active": true,
  "finish_date": "2024-12-31",
  "frequency": "monthly",
  "variant": "recurring",
  "title": "Office Supplies",
  "info": "Monthly office supply budget",
  "net_total": 500.0,
  "net_total_in_account_currency": 500.0,
  "exhausted": 250.0,
  "exhausted_in_account_currency": 250.0,
  "currency": "CHF",
  "company": {
    "id": 5552,
    "name": "Office Supplies Inc."
  },
  "cost_center": {
    "id": 123,
    "title": "Administration"
  },
  "user": {
    "id": 433109936,
    "firstname": "Mario",
    "name": "Rossi"
  },
  "purchases": [
    {
      "id": 987,
      "number": "E2024-0001",
      "date": "2024-01-15",
      "net_total": 125.0,
      "currency": "CHF",
      "status": "archived"
    }
  ],
  "create_on_recur": true,
  "recur_next_on": "2024-02-01",
  "custom_properties": { "Department": "IT" },
  "updated_at": "2024-01-15T10:30:00Z",
  "created_at": "2024-01-01T08:00:00Z"
}
```

## GET /purchase_orders

Retrieve all purchase orders:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchase_orders' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's also possible to filter:

- [Global filters apply](../entities#global-filters)
- **ids** – filter by comma-separated IDs, e.g. `?ids=123,456`

## GET /purchase_orders/{id}

Retrieve a single purchase order:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchase_orders/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Returns the complete representation for a single purchase order including all linked purchases.
