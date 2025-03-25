---
layout: default
parent: Entities
has_children: true
---

# Projects

German: "Projekte"

- TOC
{:toc}

## Attributes

The project representation contains, among the standard fields, also:

- custom properties
- project leader (user)
- customer
- deal (optional)
- tasks (services)
- contracts (assigned staff)
- project group

The attributes `hourly_rate` and `billing_variant` are linked. By choosing the billing variant "project", the hourly rate is just that. If choosing "task" (depending on the service) or "user" (depending on the staff), hourly rate becomes the mean value of hourly rates. Thus, `hourly_rate` on a `task` or `contract` only become relevant if the `billing_variant` is set accordingly.

```json
{
  "id": 1234567,
  "identifier": "P001",
  "name": "Website Support",
  "active": true,
  "billable": true,
  "fixed_price": true,
  "retainer": false,
  "start_date": null,
  "finish_date": "2018-12-31",
  "color": "#CCCC00",
  "currency": "EUR",
  "billing_variant": "project",
  "billing_address": "Beispiel AG\nHerr Maier\nBeispielstrasse...",
  "billing_email_to": "project@beispiel.co",
  "billing_email_cc": "project-cc@beispiel.co",
  "billing_notes": "Billig notes text",
  "setting_include_time_report": true,
  "budget": 18200,
  "budget_monthly": null,
  "budget_expenses": 8200,
  "hourly_rate": 150,
  "info": "Abrechnung jährlich",
  "tags": ["Print", "Digital"],
  "customer_report_url": "https://mycompany.mocoapp.com/projects/1234567/customer_report/cfd1901d23e000712488",
  "custom_properties": {
    "Project Management": "https://basecamp.com/123456"
  },
  "leader": {
    "id": 933590696,
    "firstname": "Michael",
    "lastname": "Mustermann"
  },
  "co_leader": null,
  "customer": {
    "id": 1233434,
    "name": "Beispiel AG"
  },
  "deal": {
    "id": 5635453,
    "name": "Website Relaunch"
  },
  "tasks": [
    {
      "id": 125112,
      "name": "Project Management",
      "billable": true,
      "active": true,
      "budget": null,
      "hourly_rate": 0,
      "description": "A task description"
    },
    {
      "id": 125111,
      "name": "Development",
      "billable": true,
      "active": true,
      "budget": null,
      "hourly_rate": 0,
      "description": "A task description"
    }
  ],
  "contracts": [
    {
      "id": 458639048,
      "user_id": 933590696,
      "firstname": "Michael",
      "lastname": "Mustermann",
      "billable": true,
      "active": true,
      "budget": null,
      "hourly_rate": 0
    },
    {
      "id": 458672097,
      "user_id": 933589591,
      "firstname": "Nicola",
      "lastname": "Piccinini",
      "billable": true,
      "active": true,
      "budget": null,
      "hourly_rate": 0
    }
  ],
  "project_group": {
    "id": 456687,
    "name": "Webpages"
  },
  "billing_contact": {
    "id": 1234,
    "firstname": "Maxine",
    "lastname": "Muster"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /projects

Retrieve all projects:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete project information (see Attributes).

The following parameters can be supplied:

- [Global filters apply](../entities#global-filters)
- **include_archived** – true/false
- **include_company** – true/false (returns a complete company instead of just ID and name)
- **leader_id** – 123456 (project (co-)leader user ID)
- **company_id** – 123456 (company ID)
- **created_from** – "2018-01-01"
- **created_to** – "2018-12-31"
- **updated_from** – "2018-01-01"
- **updated_to** – "2018-12-31"
- **tags** – "Important, Strategic" (comma separated list)
- **identifier** – "P1903-003"
- **retainer** – true/false
- **project_group_id** – e.g. `4566687`

## GET /projects/assigned

Retrieve all projects assigned to the user:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/assigned' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with limited project information.

```json
[
  {
    "id": 1234,
    "identifier": "P1900",
    "name": "Application",
    "active": false,
    "billable": true,
    "customer": {
      "id": 4567,
      "name": "A Company"
    },
    "tasks": [
      {
        "id": 573383,
        "name": "Integrations",
        "active": true,
        "billable": true
      }
    ],
    "contract": {
      "user_id": 65455,
      "active": true
    }
  }
]
```

The following parameters can be supplied:

- **active** – true/false

## GET /projects/{id}

Retrieve a single project:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns a single project representation.

## POST /projects

Create a project:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/projects' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Website Relaunch",
        "currency": "EUR",
        "leader_id": "1234",
        "customer_id": "5678",
        "tags": ["Print", "Digital"],
      }'
```

Mandatory fields are marked with a star (\*):

- **name\*** – "Relaunch Website"
- **currency\*** – "EUR"
- **start_date\*** – "2018-01-01"
- **finish_date\*** – "2018-12-31"
- **fixed_price\*** – true/false
- **retainer\*** – true/false ⚠ see below requirements for other fields
- **leader_id\*** – 123456 (user ID)
- **co_leader_id** – 12345 (user ID)
- **customer_id\*** – 234567
- **deal_id** – 123456 (deal ID)
- **contact_id** - 123456 (contact ID)
- **secondary_contact_id** - 56789 (contact ID)
- **billing_contact_id** - 56789 (contact ID)
- **identifier\*** – "P-123" (only mandatory if number ranges are manual)
- **billing_address** – "Beispiel AG\nBeispielstrasse 123\n12345 Berlin"
- **billing_email_to** - "project@beispiel.co"
- **billing_email_cc** - "project-cc@beispiel.co"
- **billing_notes** - "Billing notes text"
- **setting_include_time_report** - true / false
- **billing_variant** – "project", "task" or "user" (default: "project")
- **hourly_rate** – 150
- **budget** – 20000
- **budget_monthly** – 2000
- **budget_expenses** - 5000
- **tags** – ["Print", "Digital"]
- **custom_properties** – {"PO-Nummer": "123-ABC"}
- **info** – "Info for this project"

{: .note }
If the field `retainer` is true, the fields `start_date`, `finish_date`, `budget_monthly` are mandatory. Also the start date has to be on the first and the finish date on the last of a month!

## PUT /projects/{id}

Update a project:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "budget": 25000
      }'
```

Fields are analogous to the POST request, except for `currency` which cannot be modified after creation.

## DELETE /projects/{id}

{: .note }
Deletes a project. It's possible only if there are no activities, invoices, offers or expenses.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## PUT /projects/{id}/archive

Archival of a project:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/archive' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json'
```

## PUT /projects/{id}/unarchive

Reactivate an archived project:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/unarchive' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json'
```

## GET /projects/{id}/report

Retrieve a project report:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/report' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns the most important project business indicators:

```json
{
  "budget_total": 50000.0,
  "budget_progress_in_percentage": 50,
  "budget_remaining": 25.0,
  "invoiced_total": 27885.0,
  "currency": "EUR",
  "hours_total": 1500,
  "hours_billable": 1340,
  "hours_remaining": 1500,
  "costs_expenses": 4000.0,
  "costs_activities": 16450.0,
  "costs_by_task": [
    {
      "id": 7536,
      "name": "Project Management",
      "hours_total": 12.5,
      "total_costs": 725.0
    },
    {
      "id": 7239,
      "name": "Design",
      "hours_total": 71.98,
      "total_costs": 5598.0
    },
    {
      "id": 573376,
      "name": "Development",
      "hours_total": 94.48,
      "total_costs": 9448.0
    }
  ]
}
```

{: .note }
All costs are in the account's main currency, it might differ from the budget and billable items!

## PUT /projects/{id}/share

Activate project report sharing:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/share' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json'
```

This returns the the following attributes:

```json
{
  "id": 123,
  "active": true,
  "url": "https://..."
}
```

## PUT /projects/{id}/disable_share

Deactive project report sharing:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/disable_share' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json'
```

This returns the the following attributes:

```json
{
  "id": 123,
  "active": false,
  "url": null
}
```

## PUT /projects/{id}/assign_project_group

Assign this project to a project group:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/assign_project_group' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
      "project_group_id": 123
    }'
```

## PUT /projects/{id}/unassign_project_group

Unassign this project from its project group:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/projects/{id}/unassign_project_group' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json'
```
