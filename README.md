# Moco API Documentation

This is the official API documentation for mocoapp.com.

## Table of Contents

- [General](#general)
- [Entities](#entities)
- [Authentication](#authentication)
- [Client Implementations / API Wrappers](#client-implementations-api-wrapper)
- [Impersonation](#impersonation)
- [Rate Limiting](#rate-limiting)
- [Pagination](#pagination)
- [Errors and HTTP status codes](#errors-and-http-status-codes)
- [Sorting](#sorting)
- [Custom Fields](#custom-fields)
- [WebHooks](#webhooks)

## General

- Data to MOCO is sent as JSON (Content-Type: application/json) and also represented as JSON
- All requests have to be [authenticated](#authentication) with a user-specific key
- Example responses showcase the happy case, i.e. usually the `200 OK` response
- Collections are usually [paginated](#pagination)
- Zapier triggers are **not** triggered for API requests
- Timestamps `created_at` and `updated_at` are sent for all entities in UTC, as ISO8601 format.

## Entities

All the entities exposed via the API can be found in their respective sections.

- [Activities](sections/activities.md)
- [Comments](sections/comments.md)
- [Companies](sections/companies.md)
- [Contacts](sections/contacts.md)
- [Deal Categories](sections/deal_categories.md)
- [Deals / Leads](sections/deals.md)
- [Invoices](sections/invoices.md)
- [Invoice Payments](sections/invoice_payments.md)
- [Offers](sections/offers.md)
- [Projects](sections/projects.md)
- [Project Contracts](sections/project_contracts.md)
- [Project Expenses](sections/project_expenses.md)
- [Project Recurring Expenses](sections/project_recurring_expenses.md)
- [Project Tasks](sections/project_tasks.md)
- [Project Payment Schedules](sections/project_payment_schedules.md)
- [Schedules](sections/schedules.md)
- [Units / Teams](sections/units.md)
- [Users](sections/users.md)
- [User Employments](sections/employments.md)
- [User Holidays](sections/holidays.md)
- [User Presences](sections/presences.md)
- [WebHooks](sections/web_hooks.md)

## Authentication

You need an API key for authentication. Each user can find their user-specific key on mocoapp.com on their profile in the "Integrations" tab. This key is provided as an Authorization header.

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects.json' \
  -H 'Authorization: Token token=YOUR_API_KEY'
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

## Client Implementations / API Wrappers

Here's a list of API client implementations, not maintained by us. Feel free to open up a PR to point to your implementation so others can re-use it.

| Language      | Repository                               |
| ------------- |:----------------------------------------:|
| Python        | https://github.com/sommalia/moco-wrapper |

## Impersonation

By default all requests are scoped to the authenticated user. Some resources cannot be written in behalf of other users like `Activities` and `User Presences`. This reflects the behaviour in the UI. But you can login as another user provided that the authenticated user has permission to _Staff_. To achieve the same behaviour in the API, one can set the following x-header:

`X-IMPERSONATE-USER-ID=123` (user id to act in behalf of)

## Rate Limiting

You can expect to be able to fire 15 requests within a time frame of 15 seconds. If you exceed this limit, the server responds with `429 Too Many Requests`.

## Pagination

Responses are paginated with a common default of 100 entries per page. In the HTTP response header, the current page, the entries per page and the number of total entries is reported. There is also a link header to links to the consecutive page.

- **X-Page** – 3
- **X-Per-Page** – 100
- **X-Total** – 415
- **Link** – `<https://{domain}.mocoapp.com/api/v1/projects.json?page=4>; rel="next"`

If there is not Link header with `rel="next"`, the current page is the last page.

## Errors and HTTP status codes

The MOCO-API is mostly conformant with the [general HTTP status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

Here are the most comment errors you will see:

- **401 Unauthorized** - Check the error message in the response body
- **403 Forbidden** - Check your [Authentication](#authentication) or your MOCO user permission
- **404 Not Found** - Check that resource exists (maybe it was deleted in the meantime)
- **422 Unprocessable Entity** - Check the provided error message in the response body
- **429 Too Many Requests** - Check [Rate Limiting](#rate-limiting)

## Sorting

Sorting is controlled by the `sort_by` query parameter. Its value is the field name that should be sorted, followed by an optional sorting order (`asc` or `desc`, default is `asc`).

Example:

- `https://{domain}.mocoapp.com/api/v1/offers?sort_by=title desc`

## Custom Fields

MOCO supports adding custom fields to many of its resources. These custom fields are readable and writable via the `custom_properties` field.

```json5
"custom_properties": {
    "UID": "123-UID-456",
    "Branche": "Automotive"
},
```

Parameters are sent with their name as key:

```bash
curl -X POST \
  https://{domain}.mocoapp.com/api/v1/customers \
  -H 'Authorization: Token token=YOUR_API_KEY' \
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
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "custom_properties": {
          "Branchen": ["Automotive", "Banking"]
        }
      }'
```

- Single-line input – "Automotive"
- Mehrzeilige Eingabe – "A multiline input..."
- Link – "https://www..."
- Yes/No – "0", "1" (0 = No, 1 = Yes)
- Single choice – "Value"
- Multiple choice – ["Value 1", "Value 2"]

⚡ **WARNING** ⚡: If you use custom fields, all of them have to be provided. If not, any that are not transmitted will be removed.

## WebHooks

Using WebHooks, integrating any system in real time becomes possible. Events in MOCO can be assigned subscriptions. 
Whenever an event triggers, MOCO sends an HTTPS `POST` payload to the WebHook's configured URL with an HMAC SHA265 signature. 
This way, MOCOs integrity as a legitimate sender of this information can be verified. Additional headers provide context 
for the sent payload.

- **X-Moco-Target** – Activity, Customer, Project, ...
- **X-Moco-Event** – create, update, delete, archive, ...
- **X-Moco-Timestamp** – Timestamp for this event
- **X-Moco-Signature** – The signature fo this request, see comment below for details
- **X-Moco-User-Id** – The user ID that triggered this hook
- The receiver has to process the request within 10 seconds

The following example shows a WebHook triggered by an activity creation.

```
X-Moco-Target: Activity
X-Moco-Event: create
X-Moco-Timestamp: 1527170410463
X-Moco-Signature: f457bffc50e9b63f455ab107c55f2f61956550aa5525c2cfe07f574014bd8a9e
X-Moco-User-Id: 933613686
```

- We recommend http://requestbin.fullcontact.com/ for WebHook development – this services provides you with temporary
  HTTPS URLs that let you inspect any incoming WebHook data.
- WebHooks are only provided to customers after the trial phase.
- WebHooks are not guaranteed to be delivered in order. Pay attention to the provided time stamp if this is important 
  for your use case.
- The signature uses HMAC with SHA256 to sign the whole payload. The key for the signature is the 32 characters 
  hexadecimal string displayed in the web hook overview.

Sample code (Ruby) to calculate the payload signature:

```ruby
irb(main):002:0> payload = '{id: 111, description: "a description"}'
=> "{id: 111, description: \"a description\"}"
irb(main):003:0> signature_key = "1d608b9d72219b90ff2393a1d3ee0ac0"
=> "1d608b9d72219b90ff2393a1d3ee0ac0"
irb(main):004:0> payload_signature = OpenSSL::HMAC.hexdigest("SHA256", signature_key, payload)
=> "09f9ebc0adeb597cb7cb37fd72b20be0caeca6bd9fb67416b663606bd7f89183"
```

- We expect a successful response code for the Webhook request (i.e. any 2XX code), otherwise it's considered a failure
  and it's retried.
- After 500 consecutive failures a Webhook is automatically disabled.   
