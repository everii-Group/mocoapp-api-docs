---
layout: default
parent: Entities
has_children: true
---

# Deals / Leads

German: "Leads"

- TOC
{:toc}

## Attributes

The lead representation contains among standard fields also:

- Custom properties, if set
- User (representative)
- Company
- Person
- Category
- Status ("potential", "pending", "won", "lost", "dropped")

Company and person are optional. The category is only important in status "pending".

```json
{
  "id": 123,
  "name": "Website V2",
  "status": "pending",
  "reminder_date": "2022-09-19",
  "closed_on": null,
  "money": 61000,
  "currency": "CHF",
  "info": "Interesting Lead!",
  "custom_properties": {
    "Type": "Website"
  },
  "user": {
    "id": 933593033,
    "firstname": "Nicola",
    "lastname": "Piccinini"
  },
  "company": {
    "id": 760260535,
    "name": "Beispiel AG",
    "type": "customer"
  },
  "person": {
    "id": 123311,
    "name": "Max Muster"
  },
  "category": {
    "id": 12,
    "name": "Angebot",
    "probability": 30
  },
  "service_period_from": "2022-09-01",
  "service_period_to": "2023-01-31",
  "created_at": "2021-10-17T09:33:46Z",
  "updated_at": "2012-10-17T09:33:46Z"
}
```

## GET /deals

Retrieve all leads:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/deals' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Additionally, these parameters can be supplied:

- **ids** – e.g. `123,456` (IDS, comma-separated)
- **updated_after** - e.g. `2022-09-01T14:00:00Z` ISO8601 timestamp, only records that have been updated/created after
- **status** – "potential", "pending", "won", "lost" or "dropped"
- **tags** "Important, Strategic" (comma separated list)

This returns an array with complete lead information (see attributes).

## GET /deals/{id}

Retrieve a single lead:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/deals/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

The response is a single lead representation.

## POST /deals

Create a lead:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/deals' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Beispiel AG Website Relaunch",
        "currency": "EUR",
        "money": "25000",
        "reminder_date": "2018-12-01",
        "user_id": 123,
        "deal_category_id": 456,
      }'
```

Mandatory fields are marked with a star (\*):

- **name\*** – "Beispiel AG / Website Relaunch"
- **currency\*** – "EUR"
- **money\*** – 25000
- **reminder_date\*** – "2017-08-15"
- **user_id\*** – 123
- **deal_category_id\*** – 456
- **company_id** – 789
- **person_id** – 357
- **info** – "Information for this lead..."
- **status** – "potential", "pending", "won", "lost" or "dropped" (default: "pending")
- **closed_on** – "2021-12-27"
- **service_period_from** – "2022-06-01" ⚠️ must be the first of the month
- **service_period_to** – "2022-12-31" ⚠️ must be the last of the month
- **tags** – ["Important", "Health"]

## PUT /deals/{id}

Update a lead:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/deals/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "status": "lost"
      }'
```

Fields are analogous to the POST request.
