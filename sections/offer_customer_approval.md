---
layout: default
parent: Offers
grand_parent: Entities
---

# Offer Customer Approval

German: "Kundenfreigabe"

- TOC
{:toc}

## Attributes

```json
{
  "id": 123,
  "offer_document_url": "/offers/456/customer_approvals/abcdefhijklmnopqrstuvwxyz1234567890/document.pdf",
  "active": false,
  "customer_full_name": null,
  "customer_email": null,
  "signature_url": null,
  "signed_at": null,
  "created_at": "2024-04-10T08:41:48Z",
  "updated_at": "2024-04-10T09:49:43Z"
}
```

## GET /offers/{id}/customer_approval

Retrieve an activated customer_approval:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/offers/{id}/customer_approval' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns the customer approval information (see Attributes) or a 404 if not yet activated.
Evaluate the `signed_at` field to verify if approval was given.

## POST /offers/{id}/customer_approval

Activate a customer approval to generate the `offer_document_url` which can be shared with the customer.

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/offers/{id}/customer_approval' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns the customer approval information (see Attributes).

## PUT /offers/{id}/customer_approval/deactivate

Deactivate a customer approval to prevent access/signing.

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/offers/{id}/customer_approval/deactivate' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
```

This returns the updated customer approval information (see Attributes).
