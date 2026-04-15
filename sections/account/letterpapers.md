---
layout: default
title: Letter Papers
parent: Account
grand_parent: Entities
---

# Letter Papers

German: "Briefpapier"

- TOC
{:toc}

## Attributes

```json
{
  "id": 123,
  "name": "Corporate Design",
  "default": true,
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /account/letterpapers

Retrieve all letter papers:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/letterpapers' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

returns an array of letter papers.

The letter paper ID can be used as `letter_paper_id` parameter when generating PDF documents (e.g. for invoices or offers).
