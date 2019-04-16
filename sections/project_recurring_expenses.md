# Project Recurring Expenses

German: "Projekte / Wiederkehrende Zusatzleistungen"

## Attributes

The representation contains, among the standard fields, also:

- Custom properties

```json
{
  "id": 47266,
  "start_date": "2017-07-01",
  "finish_date": "2017-12-31",
  "recur_next_date": "2017-09-01",
  "period": "monthly",
  "title": "Hosting XS",
  "description": "<div>Hosting, Monitoring und Backup</div>",
  "quantity": 1,
  "unit": "Server",
  "unit_price": 29,
  "unit_cost": 19,
  "price": 29,
  "cost": 19,
  "currency": "CHF",
  "budget_relevant": true,
  "billable": true,
  "custom_properties": {
    "Type": "Website"
  },
  "created_at": "2018-10-17 09:33:46 UTC",
  "updated_at": "2018-10-17 09:33:46 UTC"
}
```

## GET /projects/{id}/recurring_expenses

Retrieve all recurring additional services entries on a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/recurring_expenses' \
  -H 'Authorization: Token token={api-key}'
```

This returns an array of recurring additional services entries (see Attributes).

## GET /projects/{id}/recurring_expenses/{id}

Retrieve a single recurring additional services entry on a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/recurring_expenses/{id}' \
  -H 'Authorization: Token token={api-key}'
```

## POST /projects/{id}/recurring_expenses

Create a recurring additional services entry on a project:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/recurring_expenses' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "start_date": "2018-10-01",
        "period": "monthly",
        "title": "Hosting XS",
        "quantity": 1,
        "unit": "Server",
        "unit_price": 29,
        "unit_cost": 19
      }'
```

Mandatory fields are marked with a star (\*):

- **start_date\*** – "2018-07-01"
- **period\*** – "weekly", "biweekly", "monthly", "quarterly", "biannual" or "annual"
- **title\*** – "Hosting XS"
- **quantity\*** – 1
- **unit\*** – "Server"
- **unit_price\*** – 29
- **unit_cost\*** – 19
- **finish_date** – "2018-12-31" (if empty: unlimited)
- **description** – "Hosting, Monitoring, Backup"
- **billable** – true/false (default: true)
- **budget_relevant** – true/false (default: false)
- **custom_properties** – {"Type": "Website"}

## PUT /projects/{id}/recurring_expenses/{id}

Update a recurring additional services entry on a project:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/recurring_expenses/{id}' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "unit_price": 49,
      }'
```

The fields are analogous to the POST request, except for `start_date` and `period`. These fields cannot be modified after creation.

## DELETE /projects/{id}/recurring_expenses/{id}

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/recurring_expenses/{id}' \
  -H 'Authorization: Token token={api-key}'
```
