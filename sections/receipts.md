# Receipts

German: "Spesen"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /receipts](#get-receipts)
- [GET /receipts/{id}](#get-receiptsid)
- [POST /receipts](#post-receipts)
- [PATCH /receipts/{id}](#patch-receiptsid)
- [DELETE /receipts/{id}](#delete-receiptsid)

<!-- /TOC -->

## Attributes

Includes among the standard fields for receipts also:

- User
- Items (with vat code, project, refund request and purchase category info)

```json
{
  "id": 123,
  "title": "Team-Lunch",
  "date": "2021-12-13",
  "billable": false,
  "pending": false,
  "gross_total": 56.5,
  "currency": "CHF",
  "items": [
    {
      "gross_total": 56.5,
      "vat": {
        "id": 186,
        "tax": 7.7,
        "reverse_charge": false,
        "intra_eu": false
      },
      "purchase_category": {
        "id": 2684,
        "name": "Bewirtungsaufwände"
      }
    }
  ],
  "project": {
    "id": 567,
    "name": "Intern/Admin",
    "billable": false,
    "company": {
      "id": 789,
      "name": "Acme Inc."
    }
  },
  "refund_request": {
    "id": 266,
    "status": "paid"
  },
  "info": "Teamlunch mit Peter, Sandra und Till",
  "user": {
    "id": 933,
    "firstname": "Sabine",
    "lastname": "Schäuble"
  },
  "attachment_url": "/system/documents/account/123/document/123/d8fef77df35c5753.pdf"
}
```

## GET /receipts

Retrieve all receipts:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/receipts' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's also possible to filter:

- **ids** – e.g. `123,456` (IDS, comma-separated)
- **updated_after** - e.g. `2022-09-01T14:00:00Z` ISO8601 timestamp, only records that have been updated/created after
- **from** – "2021-06-01"
- **to** – "2021-06-30"
- **project_id** – 567 (Project ID)
- **user_id** – 933 (User ID)
- **purchase_category_id** – 2684 (Purchase Category ID)
- **submitted** – true/false (refund request created)

Returns an array with all receipt information (see attributes).

## GET /receipts/{id}

Retrieve a single receipt:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/receipts/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Returns the representation for a single receipt.

## POST /receipts

Create a receipt:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/receipts' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '
    {
      "date": "2020-02-02",
      "title": "Lunch with coworkers",
      "items": [
        {
          "vat_code_id": 186,
          "gross_total": 99.90
        }
      ],
      "project_id": 123,
      "attachment": {
        "filename": "document.pdf",
        "base64": "JVBERi0xLjQKJeLjz9MKNCAwIG9iago8PC9GaWx..."
      }
    }'
```

Mandatory fields are marked with a star (\*):

- **date\*** – "2020-02-02"
- **title\*** – "Lunch with coworkers"
- **items\*** – list of positions. At least one position must be present and every position has the following fields:
  - **vat_code_id\*** – 186 (Vat Code ID)
  - **gross_total\*** – 99.90
- **project_id** – 123 (Project ID)
- **info** – free text
- **billable** – true/false
- **attachment** – file attached to the purchase, with the following fields:
  - **filename** – "document.pdf"
  - **base64** – base64 encoded content of the file

## PATCH /receipts/{id}

Update a receipt:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/receipts/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '
    {
      "date": "2020-02-02",
      "title": "Lunch with customer",
      "items": [
        {
          "vat_code_id": 186,
          "gross_total": 109.90
        }
      ],
      "attachment": {
        "filename": "document.pdf",
        "base64": "JVBERi0xLjQKJeLjz9MKNCAwIG9iago8PC9GaWx..."
      }
    }'
```

Fields are similar to the create action.

⚠ If provided, the field `items` will overwrite any existing items and has therefore to be provided entirely.

## DELETE /receipts/{id}

⚠ Deletes a receipt. It's possible only until no _refund_request_ has been created (receipt has not been requested for refund).

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/receipts/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
