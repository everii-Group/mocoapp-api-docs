---
layout: default
title: Fixed Costs
parent: Account
grand_parent: Entities
---

# Fixed Costs

{: .note }
This documentation is outdated, please refer to [our OpenAPI spec](https://docs.mocoapp.com/api/docs/v1#tag/accountrates).

German: "Fixkosten"

- TOC
{:toc}

## Attributes

The representation contains, among the standard fields, also:

```json
{
  "id": 123,
  "title": "Salaries",
  "description": "Monhtly total salaries for the company",
  "costs": [
    {
      "year": 2020,
      "month": 1,
      "amount": 100000.0
    },
    {
      "year": 2020,
      "month": 2,
      "amount": 100000.0
    },
    {
      "year": 2020,
      "month": 3,
      "amount": 100000.0
    }
  ],
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /account/fixed_costs

Retrieve all fixed costs

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/fixed_costs' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns complete fixed cost information (see Attributes).

Additionally, the following parameters can be supplied:

- **year** – 2020 (limit costs to a specific year)
