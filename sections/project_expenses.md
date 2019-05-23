# Project Expenses

German: "Projekte / Zusatzleistungen"

## Attributes

The representation contains, among the standard fields, also the following fields:

- Custom properties

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
  "file_url": "https//meinefirma.mocoapp.com/.../beleg1.jpg",
  "custom_properties": {
    "Type": "Website"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /projects/{id}/expenses

Retrieve all additional services for a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses' \
  -H 'Authorization: Token token={api-key}'
```

This returns an array with all additional services (see Attributes).

## GET /projects/{id}/expenses/{id}

Retrieve a single additional service for a project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses/{id}' \
  -H 'Authorization: Token token={api-key}'
```

## POST /projects/{id}/expenses

Create an additional service entry on a project:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "date": "2018-10-01",
        "title": "Hosting XS",
        "quantity": 3,
        "unit": "months",
        "unit_price": 29,
        "unit_cost": 19
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
- **custom_properties** – {"Type": "Website"}

## POST /projects/{id}/expenses/bulk

Create multiple additional services entries:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses/bulk' \
  -H 'Authorization: Token token={api-key}' \
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
  -H 'Authorization: Token token={api-key}' \
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
  -H 'Authorization: Token token={api-key}'
```

## POST /projects/{id}/expenses/disregard

Mark additional services entries as "already billed".

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/expenses/disregard' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expense_ids": [1234, 5678],
        "reason": "Courtesy services, as discussed"
      }'
```

Mandatory fields are marked with a star (\*):

- **reason\*** – "Courtesy services, as discussed"
- **expense_ids\*** – [1234, 5678]
