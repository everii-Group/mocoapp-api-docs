# Project Recurring Expenses

German: "Projekte / Wiederkehrende Zusatzleistungen"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /recurring_expenses](#get-recurring_expenses)
- [GET /projects/{id}/recurring_expenses](#get-projectsidrecurring_expenses)
- [GET /projects/{id}/recurring_expenses/{id}](#get-projectsidrecurring_expensesid)
- [POST /projects/{id}/recurring_expenses](#post-projectsidrecurring_expenses)
- [PUT /projects/{id}/recurring_expenses/{id}](#put-projectsidrecurring_expensesid)
- [DELETE /projects/{id}/recurring_expenses/{id}](#delete-projectsidrecurring_expensesid)

<!-- /TOC -->

## Attributes

The representation contains, among the standard fields, also:

- Custom properties
- Project

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
  "service_period_direction": "forward",
  "custom_properties": {
    "Type": "Website"
  },
  "project": {
    "id": 1234,
    "name": "Project A"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /recurring_expenses

Retrieve all recurring additional services entries, or all the recurring additional service entries on a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/recurring_expenses' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
This returns an array of recurring additional services entries (see Attributes).

## GET /projects/{id}/recurring_expenses

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/recurring_expenses' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array of recurring additional services entries for the project (see Attributes).

## GET /projects/{id}/recurring_expenses/{id}

Retrieve a single recurring additional services entry on a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/recurring_expenses/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /projects/{id}/recurring_expenses

Create a recurring additional services entry on a project:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/recurring_expenses' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "start_date": "2018-10-01",
        "period": "monthly",
        "service_period_direction": "forward",
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
- **service_period_direction** – "none", "forward", "backward" (default: "none")
- **custom_properties** – {"Type": "Website"}

## PUT /projects/{id}/recurring_expenses/{id}

Update a recurring additional services entry on a project:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/recurring_expenses/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
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
  -H 'Authorization: Token token=YOUR_API_KEY'
```
