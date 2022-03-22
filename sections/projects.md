# Projects

German: "Projekte"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /projects](#get-projects)
- [GET /projects/assigned](#get-projectsassigned)
- [GET /projects/{id}](#get-projectsid)
- [POST /projects](#post-projects)
- [PUT /projects/{id}](#put-projectsid)
- [DELETE /projects/{id}](#delete-projectsid)
- [PUT /projects/{id}/archive](#put-projectsidarchive)
- [PUT /projects/{id}/unarchive](#put-projectsidunarchive)
- [GET /projects/{id}/report](#get-projectsidreport)

<!-- /TOC -->

## Attributes

The project representation contains, among the standard fields, also:

- custom properties
- project leader (user)
- customer
- deal (optional)
- tasks (services)
- contracts (assigned staff)

The attributes `hourly_rate` and `billing_variant` are linked. By choosing the billing variant "project", the hourly rate is just that. If choosing "task" (depending on the service) or "user" (depending on the staff), hourly rate becomes the mean value of hourly rates. Thus, `hourly_rate` on a `task` or `contract` only become relevant if the `billing_variant` is set accordingly.

```json
{
  "id": 1234567,
  "identifier": "P001",
  "name": "Website Support",
  "active": true,
  "billable": true,
  "fixed_price": true,
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
  "budget_expenses": 8200,
  "hourly_rate": 150,
  "info": "Abrechnung jährlich",
  "tags": ["Print", "Digital"],
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
      "hourly_rate": 0
    },
    {
      "id": 125111,
      "name": "Development",
      "billable": true,
      "active": true,
      "budget": null,
      "hourly_rate": 0
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

- **include_archived** – true/false
- **include_company** – true/false (returns a complete company instead of just ID and name)
- **leader_id** – 123456 (project (co-)leader user ID)
- **company_id** – 123456 (company ID)
- **created_from** – "2018-01-01"
- **created_to** – "2018-12-31"
- **updated_from** – "2018-01-01"
- **updated_to** – "2018-12-31"
- **tags** "Important, Strategic" (comma separated list)
- **identifier** "P1903-003"

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
    ]
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
- **finish_date\*** – "2018-12-31"
- **leader_id\*** – 123456 (user ID)
- **co_leader_id\** – 123457 (user ID)
- **customer_id\*** – 234567
- **deal_id** – 123456 (deal ID)
- **identifier\*** – "P-123" (only mandatory if number ranges are manual)
- **billing_address** – "Beispiel AG\nBeispielstrasse 123\n12345 Berlin"
- **billing_email_to** - "project@beispiel.co"
- **billing_email_cc** - "project-cc@beispiel.co"
- **billing_notes** - "Billing notes text"
- **setting_include_time_report** - true / false
- **billing_variant** – "project", "task" or "user" (default: "project")
- **hourly_rate** – 150
- **budget** – 20000
- **tags** – ["Print", "Digital"]
- **custom_properties** – {"PO-Nummer": "123-ABC"}
- **info** – "Info for this project"

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

⚠ Deletes a project. It's possible only if there are no activities, invoices, offers or expenses.

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

⚠ All costs are in the account's main currency, it might differ from the budget and billable items!
