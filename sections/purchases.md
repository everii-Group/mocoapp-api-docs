# Purchases

German: "Ausgaben"

## Attributes

Includes among the standard fields for purchases also:

- Tags
- Company (if the purchase is associated to a supplier)
- Payments (list of payments made for the purchase)
- User
- Items

```json5
{
  "id": 987,
  "identifier": "E2016-0001",
  "receipt_identifier": "KK121",
  ",title": "SBB Ticket",
  "info": null,
  "iban": "CH3908704016075473007",
  "reference": null,
  "date": "2020-02-28",
  "due_date": null,
  "service_period_from": "2020-02-28",
  "service_period_to": "2020-02-28",
  "status":"pending",
  "payment_method": "bank_transfer",
  "net_total": 44.88,
  "gross_total": 46.0,
  "currency": "CHF",
  "file_url": null,
  "custom_properties": {"Various": "some stuff"}
  "tags": ["Transportation"],
  "company": {
    "id":5552,
    "name": "Schweizerische Bundesbahnen SBB",
    "iban":"CH3908704016075473007"
  },
  "payments": [],
  "user": {
    "id":433109936,
    "firstname":"Mario",
    "name":"Rossi"
  },
  "items": [
    {
      "id": 311936153,
      "title": "SBB Ticket",
      "net_total": 44.88,
      "tax_total": 1.12,
      "tax": 2.5,
      "tax_included": true,
      "gross_total": 46.0,
      "category": {
        "id": 671034328,
        "name": "Spesen und Reisekosten",
        "credit_account": "6640"
      },
      "supplier_credit_number": 70001
    }
  ]
}
```

## GET /purchases

Retrieve all purchases:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's also possible to filter:

- **id** – identifier of the purchase,
- **category_id** – identifier of the purchases' category,
- **term** – full text search on purchase positions,
- **company_id** – identifier of the supplier, pass _0_ to get the purchases not associated to a supplier,
- **status** – "pending" or "approved", 
- **tags** – "Transportation, Restaurants" (comma separated list)
- **date** – date range in the form _2020-02-01:2020-02-22_
- **unpaid** – filter only purchases without a payment

Returns an array with all purchases information (see attributes).

## GET /purchases/{id}

Retrieve a single purchase:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Returns the representation for a single purchase.

## POST /purchases

Create a purchase:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/purchases' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '
    {
      "date": "2020-02-02",
      "currency": "EUR",
      "payment_method": "bank_transfer",
      "receipt_identifier": "XXLA",
      "custom_properties": { "Various" => "Stuff" },
      "items": [
        {
          "title": "Ticket",
          "total": 30,
          "tax": 10,
          "tax_included": true,
        }
      ],
      "file": {
        "filename": "document.pdf",
        "base64": "JVBERi0xLjQKJeLjz9MKNCAwIG9iago8PC9GaWx..."
      }
    }'
```

Mandatory fields are marked with a star (\*):

- **date\*** – "2020-02-02"
- **currency\*** – "F", "M" or "U"
- **payment_method\*** – "bank_transfer", "direct_debit", "credit_card", "paypal", "cash"
- **items\*** – list of position. At least one position must be present and every position has the following fields:
  - **title\*** – Ticket
  - **total\*** – 30
  - **tax\*** – 7.7 (tax percentage)
  - **tax_included** – true (specify if the total includes the tax or not) 
- **due_date** – "2020-02-18"
- **service_period_from** – "2020-01-01"
- **service_period_to** – "2020-01-31"
- **due_date** – "2020-02-18"
- **company_id** – 211 (reference to the supplier)
- **receipt_identifier** – 123
- **info** – free text
- **iban** – CH123
- **reference** – ref
- **custom_property_values** – {"Field": "Value}
- **file** – file attached to the purchase, with the following fields:
  - filename – "document.pdf"
  - base64 – base64 encoded content of the file
- **tags** – ["Label1", "Label2"]

## DELETE /purchases/{id}

⚠ Deletes a purchase. It's possible only if the status is _pending_ and no payments have been registered.

## PATCH /purchases/{id}/update_status

Updates the purchase status:

```bash
curl -X PATCH \
  'https://{domain}.mocoapp.com/api/v1/purchases/123' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '
    {
      "status": "approved"
    }'
```

- **status\*** – "pending", "approved"

## PATCH /purchases/{id}/store_document

Submits the purchase's document using `multipart/form-data` format if it has to be changed afterwards or was not submitted 
with the initial creation.


```bash
curl -X PATCH \
  'https://{domain}.mocoapp.com/api/v1/purchases/123' \
  -F file=@PATH_TO_FILE
```

- **file\*** – the document to store

