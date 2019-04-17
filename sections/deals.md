# Deals / Leads

German: "Leads"

## Attributes

The lead representation contains among standard fields also:

- Custom properties, if set
- User (representative)
- Customer – DEPRECATED: use Company
- Company
- Category
- Status ("potential", "pending", "won", "lost", "dropped")

The company is optional. The category is only important in status "pending".

```json
{
  "id": 123,
  "name": "Website V2",
  "status": "pending",
  "reminder_date": "2017-05-19",
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
    "type": "Customer"
  },
  "category": {
    "id": 12,
    "name": "Angebot",
    "probability": 30
  },
  "created_at": "2018-10-17 09:33:46 UTC",
  "updated_at": "2018-10-17 09:33:46 UTC"
}
```

## GET /deals

Retrieve all leads:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/deals' \
  -H 'Authorization: Token token={api-key}'
```

Additionally, these parameters can be supplied:

- **status** – "potential", "pending", "won", "lost" or "dropped"

This returns an array with complete lead information (see attributes).

## GET /deals/{id}

Retrieve a single lead:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/deals/{id}' \
  -H 'Authorization: Token token={api-key}'
```

The response is a single lead representation.

## POST /deals

Create a lead:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/deals' \
  -H 'Authorization: Token token={api-key}' \
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
- **info** – "Information for this lead..."
- **status** – "potential", "pending", "won", "lost" or "dropped" (default: "pending")

## PUT /deals/{id}

Update a lead:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/deals/{id}' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "status": "lost"
      }'
```

Fields are analogous to the POST request.
