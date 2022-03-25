# Project Expenses

German: "Projekte / Zusatzleistungen"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /projects/{id}/expenses](#get-projectsidexpenses)
- [GET /projects/{id}/expenses/{id}](#get-projectsidexpensesid)
- [POST /projects/{id}/expenses](#post-projectsidexpenses)
- [POST /projects/{id}/expenses/bulk](#post-projectsidexpensesbulk)
- [PUT /projects/{id}/expenses/{id}](#put-projectsidexpensesid)
- [DELETE /projects/{id}/expenses/{id}](#delete-projectsidexpensesid)
- [POST /projects/{id}/expenses/disregard](#post-projectsidexpensesdisregard)
- [GET /projects/expenses](#get-projectsexpenses)

<!-- /TOC -->

## Attributes

The representation contains, among the standard fields, also the following fields:

- Custom properties
- Company
- Project

```json
{
  "id": 47266,
  "date": "2017-07-07",
  "title": "Hosting XS",
  "description": "<div>Hosting, Monitoring und Backup</div>",
  "quantity": 3,
  "unit": "Monat",
  "unit_price": 29,
  "unit_cost": 19,
  "price": 87,
  "cost": 57,
  "currency": "CHF",
  "budget_relevant": true,
  "billable": true,
  "billed": false,
  "service_period": "10/2020",
  "service_period_from": "2020-10-01",
  "service_period_to": "2020-10-31",
  "file_url": "https//meinefirma.mocoapp.com/.../beleg1.jpg",
  "custom_properties": {
    "Type": "Website"
  },
  "company": {
    "id": 1234,
    "name": "Acme Corp."
  },
  "project": {
    "id": 1234,
    "name": "Project A"
  },
  "purchase_id": 123456,
  "purchase_item_id": 234567,
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /projects/{id}/expenses

Retrieve all additional services for a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with all additional services (see Attributes).

## GET /projects/{id}/expenses/{id}

Retrieve a single additional service for a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /projects/{id}/expenses

Create an additional service entry on a project:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "date": "2018-10-01",
        "title": "Hosting XS",
        "quantity": 3,
        "unit": "months",
        "unit_price": 29,
        "unit_cost": 19,
        "file": {
          "filename": "document.pdf",
          "base64": "JVBERi0xLjQKJeLjz9MKNCAwIG9iago8PC9GaWx..."
        }
      }'
```

Mandatory fields are marked with a star (\*):

- **date\*** – "2017-04-12"
- **title\*** – "Hosting XS"
- **quantity\*** – 3
- **unit\*** – "months"
- **unit_price\*** – 29
- **unit_cost\*** – 19
- **description** – "Hosting, Monitoring, Backup"
- **billable** – true/false (default: true)
- **budget_relevant** – true/false (default: false)
- **service_period_from** – "2021-01-01"
- **service_period_to** – "2021-01-31"
- **custom_properties** – {"Type": "Website"}
- **file** – file attached to the expense, with the following fields:
  - filename – "document.pdf"
  - base64 – base64 encoded content of the file

## POST /projects/{id}/expenses/bulk

Create multiple additional services entries:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses/bulk' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "bulk_data": [
          {
            "date": "2018-10-20",
            "title": "Hosting: Server",
            "quantity": 1,
            "unit": "Server",
            "unit_price": 29,
            "unit_cost": 19
          },
          {
            "date": "2018-10-22",
            "title": "Hosting: Server",
            "quantity": 1,
            "unit": "Server",
            "unit_price": 29,
            "unit_cost": 19
          }
        ]
      }'
```

Mandatory fields are marked with a star (\*):

- **date\*** – "2017-04-12"
- **title\*** – "Hosting XS"
- **quantity\*** – 3
- **unit\*** – "months"
- **unit_price\*** – 29
- **unit_cost\*** – 19
- **description** – "Hosting, Monitoring, Backup"
- **billable** – true/false (default: true)
- **budget_relevant** – true/false (default: false)

## PUT /projects/{id}/expenses/{id}

Update an additional services entry on a project:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "unit_price": 49
      }'
```

Fields are analogous to the POST request. Updates are only possible if this entry is not yet billed.

## DELETE /projects/{id}/expenses/{id}

Delete an additional services entry on a project.

Deletions are only possible if this entry is not yet billed.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /projects/{id}/expenses/disregard

Mark additional services entries as "already billed".

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses/disregard' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "expense_ids": [1234, 5678],
        "reason": "Courtesy services, as discussed"
      }'
```

Mandatory fields are marked with a star (\*):

- **reason\*** – "Courtesy services, as discussed"
- **expense_ids\*** – [1234, 5678]

## GET /projects/expenses

Retrieve all additional services

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/expenses' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with all additional services (see Attributes).

Additionally, these parameters can be supplied:

- **from** – "2019-01-01"
- **to** – "2019-01-31"
- **tags** – "tag one,tag two" (comma-separated project tags)

⚠️ Parameters `from` and `to` only work when provided together. 
