# Invoice Payments

German: "Rechnungen / Zahlungen"

## Attributes

The invoice payment representation contains among standard fields also shortened invoice information.

```json5
{
  "id": 123,
  "date": "2017-10-01",
  "invoice": {
    "id": 12345,
    "identifier": "R1710-001",
    "title": "Invoice – Website"
  },
  "paid_total": "17999.00",
  "paid_total_in_account_currency": "17999.00",
  "currency": "EUR",
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /invoices/payments

Retrieve all invoice payments:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/payments' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Additionally, these parameters can be used to filter the results set:

- **invoice_id** – 123
- **date_from** – "2018-01-01"
- **date_to** – "2018-01-31"

## GET /invoices/payments/{id}

Retrieve a single invoice payment:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/payments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /invoices/payments

Create an invoice payment:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/invoices/payments' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "date": "2018-10-20",
        "invoice_id": 123,
        "paid_total": 1000,
        "currency": "EUR"
      }'
```

Mandatory fields are marked with a star (\*):

- **date\*** – "2017-10-20"
- **invoice_id\*** – 12345
- **paid_total\*** – 1000
- **currency** – "EUR"

## POST /invoices/payments/bulk

Create multiple invoice payments in bulk:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/invoices/payments/bulk' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "bulk_data": [
          {
            "date": "2018-10-20",
            "invoice_id": 456,
            "paid_total": 2000,
            "currency": "EUR"
          },
          {
            "date": "2018-10-22",
            "invoice_id": 123,
            "paid_total": 1000,
            "currency": "EUR"
          }
        ]
      }'
```

Mandatory fields are marked with a star (\*):

- **date\*** – "2018-10-20"
- **invoice_id\*** – 12345
- **paid_total\*** – 1000
- **currency** – "EUR"

## PUT invoices/payments/{id}

Update an invoice payment:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/invoices/payments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "paid_total": 2000
      }'
```

Fields are analogous to the POST request, except for the `invoice_id`.

## DELETE /invoices/payments/{id}

Delete an invoice payment:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/invoices/payments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
