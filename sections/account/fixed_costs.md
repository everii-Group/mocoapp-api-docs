---
layout: default
title: Account / Fixed Costs
parent: Entities
---

# Fixed costs (Account)

German: "Fixkosten"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /account/fixed_costs](#get-accountfixed_costs)

<!-- /TOC -->

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
