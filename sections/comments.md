---
layout: default
parent: Entities
---

# Comments

German: "Notizen"

- TOC
{:toc}

## Attributes

The representation contains, among the standard fields, also:

- user (creator)

```json
{
  "id": 123,
  "commentable_id": 12345,
  "commentable_type": "Project",
  "text": "<div>Project was ordered on <strong>1.10.2017</strong></div>.",
  "manual": true,
  "user": {
    "id": 567,
    "firstname": "Tobias",
    "lastname": "Miesel"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

The text must be "plain text" or valid HTML. MOCO removes all HTML-tags, except for `['div', 'strong', 'em', 'u', 'pre', 'ul', 'ol', 'li', 'br']`.

## GET /comments

Retrieve all comments

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/comments' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns complete comment information (see Attributes).

Additionally, the following parameters can be supplied:

- **ids** – e.g. `123,456` (IDS, comma-separated)
- **commentable_type** – "Company", "Contact", "Deal", "DeiveryNote", "Expense", "Invoice", "InvoiceBookkeepingExport", "InvoiceDeletion", "InvoiceReminder", "Offer", "OfferConfirmation", "Project", "ProjectGroup", "Purchase", "PurchaseBookkeepingExport", "PurchaseDraft", "Receipt", "ReceiptRefundRequest", "RecurringExpense", "Unit", "User", "UserHolidayRequest" (object this comment relates to)
- **commentable_id** – 123 (object ID)
- **user_id** – 456 (creator user ID)
- **manual** – true/false (user-created or generated)

## GET /comments/{id}

Retrieve a single comment:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/comments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns a single comment representation.

## POST /comments

Create a comment:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/comments' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "commentable_id": 123,
        "commentable_type": "Project",
        "text": "<div>Project was ordered on <strong>1.10.2017</strong></div>."
      }'
```

Mandatory fields are marked with a star (\*):

- **commentable_id\*** – 123 (object ID)
- **commentable_type\*** – ""Contact", "Deal", "DeliveryNote", "Project", "User", "Unit", "Company", "Offer", "OfferConfirmation", "Invoice", "InvoiceReminder", "InvoiceDeletion", "InvoiceBookkeepingExport", "Expense", "RecurringExpense", "Receipt", "ReceiptRefundRequest", "Purchase", "PurchaseBookkeepingExport", "PurchaseDraft" (object type)
- **text\*** – "Comment text..."
- **attachment_filename** – "document.pdf"
- **attachment_content** – _the file as a base64-encoded string_

## POST /comments/bulk

Create multiple comments in bulk:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/comments/bulk' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "commentable_ids": [123, 234, 345],
        "commentable_type": "Contact",
        "text": "Sent Newsletter RJ-2019/03"
      }'
```

Mandatory fields are marked with a star (\*):

- **commentable_ids\*** – [123, 234, ...] (object IDs)

Other fields are analogous to the POST request.

## PUT /comments/{id}

Update a comment:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/comments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "text": "<div>Project is paused for now.</div>.",
      }'
```

Fields are analogous to the POST request.

## DELETE /comments/{id}

Deleting manually created comments:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/comments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
