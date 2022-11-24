---
layout: default
title: Account / Internal Hourly Rates
parent: Entities
---

# Internal Hourly Rates

German: "Interne Stundensätze"

- TOC
{:toc}

## GET /account/internal_hourly_rates

Retrieve internal hourly rates:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/internal_hourly_rates' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

The following parameters can be supplied:

- **years** – 2021 or 2020,2021 (single year or multiple years comma-separated)
- **unit_id** – 1234

returns:

```json
[
  {
    "id": 933589613,
    "full_name": "Daniela Demo",
    "rates": [
      {
        "year": 2020,
        "rate": 120.0
      },
      {
        "year": 2021,
        "rate": 130.0
      }
    ]
  },
  {
    "id": 933618769,
    "full_name": "Max Muster",
    "rates": [
      {
        "year": 2020,
        "rate": 110.0
      },
      {
        "year": 2021,
        "rate": 120.0
      }
    ]
  }
]
```

## PATCH /account/internal_hourly_rates

Update internal hourly rates

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/account/internal_hourly_rates' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "year": 2021,
        "rates": [
          {
            "user_id": 933589613,
            "rate": 140.0
          },
          {
            "user_id": 933618769,
            "rate": 130.0
          }
        ]
      }'
```
