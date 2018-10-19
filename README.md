# Moco API Documenation

This is the official API documentation for mocoapp.com.

## Table of Contents

* [General](#general)
* [Entities](#entities)
* [Authentication](#authentication)
* [Rate Limiting](#rate-limiting)
* [Pagination](#pagination)
* [Sorting](#sorting)
* [Custom Fields](#custom-fields)
* [WebHooks](#webhooks)

## General

* Data to MOCO is sent as JSON (Content-Type: application/json) and also represented as JSON
* All requests have to be [authenticated](#authentication) with a user-specific key
* Example responses showcase the happy case, i.e. usually the `200 OK` response
* Collections are usually [paginated](#pagination)
* Zapier triggers are **not** triggered for API requests

## Entities

All the entities exposed via the API can be found in their respective sections.

* [Activities](sections/activities.md)
* [Comments](sections/comments.md)
* [Companies](sections/companies.md)
* [Contacts](sections/contacts.md)
* [Deals / Leads](sections/deals.md)
* [Invoices](sections/invoices.md)
* [Invoice Payments](sections/invoice_payments.md)
* [Offers](sections/offers.md)
* [Projects](sections/projects.md)
* [Project Contracts](sections/project_contracts.md)
* [Project Expenses](sections/project_expenses.md)
* [Project Recurring Expenses](sections/project_recurring_expenses.md)
* [Project Tasks](sections/project_tasks.md)
* [Schedules](sections/schedules.md)
* [Units / Teams](sections/units.md)
* [Users](sections/users.md)

## Authentication

You need an API key for authentication. Each user can find their user-specific key on mocoapp.com on their profile in the "Integrations" tab. This key is provided as an Authorization header.

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects.json' \
  -H 'Authorization: Token token={api-key}'
```

This key can also be requested via API:

```bash
curl -X POST \
  https://{domain}.mocoapp.com/api/v1/session \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "email": "max@muster.de",
    "password": "secret"
  }'
```

## Rate Limiting

You can expect to be able to fire 15 requests within a time frame of 15 seconds. If you exceed this limit, the server responds with `429 Too Many Requests`.

## Pagination

Responses are paginated with a common default of 100 entries per page. In the HTTP response header, the current page, the entries per page and the number of total entries is reported. There is also a link header to links to the consecutive page.

* **X-Page** – 3
* **X-Per-Page** – 100
* **X-Total** – 415
* **Link** – `<https://{domain}.mocoapp.com/api/v1/projects.json?page=4>; rel="next"`

If there is not Link header with `rel="next"`, the current page is the last page.

## Sorting

Sorting is controlled by the `sort_by` query parameter. Its value is the field name that should be sorted, followed by an optional sorting order (`asc` or `desc`, default is `asc`).

Example:

* `https://{domain}.mocoapp.com/api/v1/offers?sort_by=title desc`

## Custom Fields

MOCO supports adding custom fields to many of its resources. These custom fields are readable and writable via the `custom_properties` field.

```json
"custom_properties": {
    "UID": "123-UID-456",
    "Branche": "Automotive"
},
```


Parameters are sent with their name as key:

```bash
curl -X POST \
  https://{domain}.mocoapp.com/api/v1/customers \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Beispiel AG",
    "currency": "CHF",
    "custom_properties": {
      "Branche": "Automotive"
    }
  }'
```

All values are encoded as strings, expect for Multiple Choice, which is encoded as an array.

```bash
curl -X POST \
  https://{domain}.mocoapp.com/api/v1/customers \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "custom_properties": {
          "Branchen": ["Automotive", "Banking"]
        }
      }'
```

* Single-line input – "Automotive"
* Mehrzeilige Eingabe – "A multiline input..."
* Link – "https://www..."
* Yes/No – "0", "1" (0 = No, 1 = Yes)
* Single choice – "Value"
* Multiple choice – ["Value 1", "Value 2"]

⚡ **WARNING** ⚡: If you use custom fields, all of them have to be provided. If not, any that are not transmitted will be removed.

## WebHooks

Using WebHooks, integrating any system in real time becomes possible. Events in MOCO can be assigned subscriptions. Whenever an event triggers, MOCO sends and HTTPS `POST` payload to the WebHook's configured URL with a SHA265 signature. This way, MOCOs integrity as a legitimate sender of this information can be verified. Additional headers provide context for the sent payload.

* **X-Moco-Target** – Activity, Customer, Project, ...
* **X-Moco-Event** – create, update, delete, archive, ...
* **X-Moco-Timestamp** – Timestamp for this event
* **X-Moco-Signature**
* The receiver has to process the request within 10 seconds

The following example shows a WebHook triggered by an activity creation.

```
X-Moco-Target: Activity
X-Moco-Event: create
X-Moco-Timestamp: 1527170410463
X-Moco-Signature: f457bffc50e9b63f455ab107c55f2f61956550aa5525c2cfe07f574014bd8a9e
```

* We recommend https://requestb.in for WebHook development – this services provides you with temoporary HTTPS URLs that let you inspect any incoming WebHook data
* WebHooks are only provided to customers after the trial phase
* WebHooks are not guaranteed to be delivered in order. Pay attention to the provided time stamp if this is important for your use case
