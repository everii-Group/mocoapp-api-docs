---
layout: default
title: Expense Templates
parent: Account
grand_parent: Entities
---

# Expense Templates

German: "Zusatzleistungs-Katalog"

- TOC
{:toc}

## Attributes

Item attributes:

- **title**
- **description**
- **unit** e.g. "hours", "pieces", "month"
- **unit_price** price for a single unit
- **unit_cost** internal cost for 1 unit
- **currency**

```json
{
  "id": 1,
  "title": "Hosting L",
  "description": "The large hosting package",
  "unit": "month",
  "unit_price": "50.0",
  "unit_cost": "40.0",
  "currency": "EUR",
  "created_at": "2022-09-17T18:14:31Z",
  "updated_at": "2022-06-24T08:17:55Z"
}
```

## GET /account/expense_templates

Retrieve expense templates:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/expense_templates' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

returns an array of expense templates.

## GET /account/expense_templates/{id}

Retrieve an expense template:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/expense_templates/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

returns a single expense template.

## POST /account/expense_templates

Create an expense template:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/account/expense_templates' \
  -H 'Authorization: Token token=YOUR_API_KEY'
  -H 'Content-Type: application/json' \
  -d '{
        "title": "Hosting S",
        "description": "The small hosting package",
        "unit": "month",
        "unit_price": "20.0",
        "unit_cost": "15.0",
        "currency": "EUR"
      }'
```

## PUT /account/expense_templates/{id}

Update an expense template:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/account/expense_templates/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
  -H 'Content-Type: application/json' \
  -d '{
        "title": "Hosting Small"
      }'
```

## DELETE /account/expense_templates/{id}

Delete an expense template:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/account/expense_templates/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
