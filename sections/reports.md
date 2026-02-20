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

- **from** - 2025-01-01, defaults to the beginning of the current year if not specified
- **to** - 2025-12-31, defaults to the end of the current year if not specified
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
  'https://{domain}.mocoapp.com/api/v1/report/finance' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's possible to filter:

- **from** - 2025-01-01, defaults to the beginning of the current year if not specified
- **to** - 2025-12-31, defaults to the end of the current year if not specified
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

## GET /report/planned_vs_tracked

Retrieve the planned vs tracked report:

```bash
curl -I -X GET \
  'https://{domain}.mocoapp.com/api/v1/report/planned_vs_tracked' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
It's possible to filter:

- **from** - 2025-01-01, defaults to the beginning of the current year if not specified
- **to** - 2025-12-31, defaults to the end of the current year if not specified
- **term** - text

This returns an array with the following structure:

```json
[
  {
    "user_id": 111,
    "project_id": 222,
    "tracked_hours": 0.0,
    "planned_hours": 218.0,
    "delta": -218.0,
    "quota": 0.0,
    "user": {
      "id": 111,
      "firstname": "John",
      "name": "Smith",
      "initials": "JS",
      "color": "#d9822b",
      "unit": {
        "id": 777,
        "name": "4 Support / Success"
      }
    },
    "project": {
      "id": 222,
      "identifier": "276",
      "name": "Support",
      "company": {
        "id": 333,
        "name": "hundertzehn GmbH"
      }
    }
  }
]
```

## GET /report/utilization

Retrieve the utilization report:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/report/utilization?from={from_date}&to={to_date}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's possible to filter:

- **from** - 2025-01-01, defaults to the beginning of the current year if not specified
- **to** - 2025-12-31, defaults to the end of the current year if not specified

```json
[
  {
    "date": "2025-08-20",
    "user_id": 92345,
    "target_hours": 6.4,
    "billable_hours": 4.3,
    "unbillable_hours": 0.83,
    "billable_seconds": 15487,
    "unbillable_seconds": 3000
  },
  {
    "date": "2025-08-21",
    "user_id": 92345,
    "target_hours": 6.4,
    "billable_hours": 2.0,
    "unbillable_hours": 3.83,
    "billable_seconds": 7200,
    "unbillable_seconds": 13800
  },
  {
    "date": "2025-08-22",
    "user_id": 92345,
    "target_hours": 6.4,
    "billable_hours": 3.33,
    "unbillable_hours": 3.5,
    "billable_seconds": 12000,
    "unbillable_seconds": 12600
  },
  {
    "date": "2025-08-20",
    "user_id": 93346,
    "target_hours": 8.0,
    "billable_hours": 0.0,
    "unbillable_hours": 0.0,
    "billable_seconds": 0.0,
    "unbillable_seconds": 0.0
  },
  {
    "date": "2025-08-21",
    "user_id": 93346,
    "target_hours": 4.0,
    "billable_hours": 0.0,
    "unbillable_hours": 0.0,
    "billable_seconds": 0.0,
    "unbillable_seconds": 0.0
  },
  {
    "date": "2025-08-22",
    "user_id": 93346,
    "target_hours": 8.0,
    "billable_hours": 0.0,
    "unbillable_hours": 0.25,
    "billable_seconds": 0,
    "unbillable_seconds": 900
  }
]
```
