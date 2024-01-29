---
layout: default
parent: Invoices
grand_parent: Entities
---

# Invoice Bookkeeping Exports

German: "Rechnungen / Buchhaltungsexporte"

- TOC
{:toc}

## Attributes

```json
{
  "id": 1101,
  "from": "2015-01-01",
  "to": "2015-12-31",
  "invoice_ids": [
    2197,
    2189,
    9771,
    2206,
    8841,
    4292,
    2204,
    2195,
    9014,
    6123,
    2205,
    8839,
    2203,
    8837,
    14447,
    2190,
    12641,
    6421,
    8836,
    2192,
    2194,
    8838,
    6124,
    2198,
    2193,
    2202,
    2199,
    2207,
    4337,
    14325,
    8840,
    2191,
    2196,
    2200,
    6122,
    2201
  ],
  "comment": "2015",
  "user": {
    "id": 933589840,
    "firstname": "Tobias",
    "lastname": "Miesel"
  },
  "status": "manual",
  "created_at": "2021-03-23T05:38:53Z",
  "updated_at": "2021-03-23T05:38:53Z"
}
```

## GET /invoices/bookkeeping_exports

Retrieve all invoice bookkeeping exports:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/bookkeeping_exports' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## GET /invoices/bookkeeping_exports/{id}

Retrieve a single invoice bookkeeping export:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/bookkeeping_exports/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /invoices/bookkeeping_exports

Create an invoice bookkeeping export:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/invoices/bookkeeping_exports' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "invoice_ids": [123, 234, 345],
      }'
```

Mandatory fields are marked with a star (\*):

- **invoice_ids\*** – [123, 234, 345]
- **trigger_submission** – true/false (e.g. submit also to DATEV; default is true)
- **comment** – "some additional info..."
