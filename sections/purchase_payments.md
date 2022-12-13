---
layout: default
parent: Purchases
grand_parent: Entities
---

# Purchase Payments

German: "Ausgaben / Zahlungen"

- TOC
{:toc}

## Attributes

The purchase payment representation contains among standard fields also shortened purchase information.

```json
{
  "id": 123,
  "date": "2022-03-01",
  "purchase": {
    "id": 12345,
    "identifier": "E2203-001",
    "title": "Purchase – Electronics"
  },
  "total": "1999.00",
  "created_at": "2022-03-01T09:33:46Z",
  "updated_at": "2022-03-01T09:33:46Z"
}
```

## GET /purchases/payments

Retrieve all purchase payments:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases/payments' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Additionally, these parameters can be used to filter the results set:

- **ids** – e.g. `123,456` (IDS, comma-separated)
- **updated_after** - e.g. `2022-09-01T14:00:00Z` ISO8601 timestamp, only records that have been updated/created after
- **purchase_id** – "123,456" (purchase IDs, can be a single one or comma-separated)
- **date_from** – "2018-01-01"
- **date_to** – "2018-01-31"

## GET /purchases/payments/{id}

Retrieve a single purchase payment:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases/payments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /purchases/payments

Create a purchase payment:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/purchases/payments' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "date": "2018-10-20",
        "purchase_id": 123,
        "total": 1000,
      }'
```

Mandatory fields are marked with a star (\*):

- **date\*** – "2017-10-20"
- **total\*** – 1000
- **purchase_id** – 12345 - ⚡ not mandatory, but if not set, `description` must be set.
- **description** – "salaries" - a description of this payment, must only be set if no `purchase_id` is set.

## POST /purchases/payments/bulk

Create multiple purchase payments in bulk:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/purchases/payments/bulk' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "bulk_data": [
          {
            "date": "2018-10-20",
            "total": 2000,
            "purchase_id": 456,
          },
          {
            "date": "2018-10-22",
            "total": 1000,
            "description": "salaries"
          }
        ]
      }'
```

Fields are analogous to the POST request.

## PUT purchases/payments/{id}

Update a purchase payment:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/purchases/payments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "total": 2000
      }'
```

Fields are analogous to the POST request, except for the `purchase_id`.

## DELETE /purchases/payments/{id}

Delete a purchase payment:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/purchases/payments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
