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

## POST /purchase_orders

Create a new purchase order:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/purchase_orders' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "date": "2026-04-29",
    "title": "Office Supplies Budget",
    "currency": "CHF",
    "user_id": 933589613,
    "net_total": 5000,
    "frequency": "once",
    "info": "Annual budget for office supplies",
    "company_id": 760554554
  }'
```

Mandatory fields are marked with a star (*):

- **date\*** – start date of the purchase order (ISO 8601)
- **title\*** – descriptive title
- **currency\*** – ISO 4217 currency code
- **user_id\*** – responsible user ID
- **net_total** – budget amount (net)
- **frequency** – `once`, `weekly`, `biweekly`, `monthly`, `quarterly`, `biannual`, `annual` (default: `once`)
- **finish_date** – end date (for recurring orders only)
- **info** – additional notes
- **company_id** – supplier company ID (optional)
- **custom_properties** – custom field values (optional)

## PUT /purchase_orders/{id}

Update an existing purchase order:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/purchase_orders/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Updated Title",
    "net_total": 6000
  }'
```

Fields are analogous to the POST request.

{: .note }
Changing the `frequency` is not allowed if purchases are already assigned to this order.

## PATCH /purchase_orders/{id}

Partially update a purchase order (only changed fields need to be provided):

```bash
curl -X PATCH \
  'https://{domain}.mocoapp.com/api/v1/purchase_orders/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "net_total": 7500
  }'
```

## DELETE /purchase_orders/{id}

Delete a purchase order:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/purchase_orders/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

{: .note }
Deleting a purchase order is only possible if **no purchases are assigned** to it. If purchases are assigned, the request will return `422 Unprocessable Content` with an error message indicating the number of assigned purchases.
