# Purchase Drafts

German: "Ausgaben – Entwürfe"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /purchases/drafts](#get-purchasesdrafts)
- [GET /purchases/drafts/{id}](#get-purchasesdraftsid)

<!-- /TOC -->

## Attributes

The purchase draft representation is:

```json
{
  "id": 123,
  "title": "Ticket",
  "email_from": "john@example.com",
  "email_body": "here the ticket",
  "user": {
    "id": 933590696,
    "firstname": "John",
    "lastname": "Doe"
  },
  "created_at": "2021-10-17T09:33:46Z",
  "updated_at": "2021-10-17T09:33:46Z"
}
```

## GET /purchases/drafts

Retrieve all drafts:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases/drafts' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete draft information (see attributes).

## GET /purchases/drafts/{id}

Retrieve a single draft:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases/drafts/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

The response is a single draft representation.
