---
layout: default
parent: Entities
---

# Reports

German: "Berichte"

- TOC
{:toc}

## GET /report/absences

Retrieve a list of absences per user:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/report/absences' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's also possible to filter:

- **active** - true/false (include only absences for active users, defaults to false)
- **year** - 2021 (defaults to current year)

This returns an array with the following structure:

```json
[
  {
    "user": {
      "id": 123,
      "firstname": "Jane",
      "lastname": "Doe"
    },
    "total_vacation_days": 25.0,
    "used_vacation_days": 10.5,
    "planned_vacation_days": 5.0,
    "sickdays": 4.0
  }
]
```

## GET /report/cashflow

Retrieve the cashflow report:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/report/cashflow' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's possible to filter:

- **from** - 2025-01-01
- **to** - 2025-12-31
- **term** - text


This returns an array with the following structure:

```json
[
  {
    "record_id": 28206351,
    "company_id": 760383472,
    "description": "R2212-022 Invoice",
    "user_id": 933622946,
    "amount_in_account_currency": 1022.07,
    "kind": "invoice_created",
    "company": {
      "id": 760683172,
      "name": "Kronenhalle Bar"
    },
    "user": {
      "id": 933622946,
      "firstname": "John",
      "lastname": "Doe"
    },
    "date": "2024-09-17"
  }
]
```

## GET /report/finance

Retrieve the finance report:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/report/cashflow' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's possible to filter:

- **from** - 2025-01-01
- **to** - 2025-12-31
- **term** - text


This returns an array with the following structure:

```json
[
  {
    "record_id": 3731655,
    "company_id": 760718470,
    "description":"ZL 1",
    "user_id": 933621267,
    "net_amount_in_account_currency": 100.0,
    "kind": "incoming_expenses",
    "company": {
      "id": 762768470,
      "name":"Maus AG"
    },
    "user": {
      "id":933621267,
      "firstname": "Jenni",
      "lastname": "Doe"
    },
    "date":"2025-03-27"
  }
]
```
