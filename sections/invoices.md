---
layout: default
parent: Entities
has_children: true
---

# Invoices

German: "Rechnungen"

- TOC
{:toc}

## Attributes

The invoice representation contains among standard fields also:

- custom properties
- positions (items)
  - type: `title`, `description`, `item`, `subtotal`, `page-break` or `separator`
  - subtotal_type: `part_total` or `sub_total` (only relevant if type is `subtotal`)
  - title: A label
  - description: A description block below that is attachted to this position
  - quantity: for detail positions, the multiplier for this position
  - unit: a label for the unit, e.g. "pieces", "hours", "days"
  - unit_price: price per unit
  - net_total: total price for position
  - additional: signifies that this is an expense (`true` / `false`)
- payments
- reminders
- user
- `vat` (`tax`, `reverse_charge`, `intra_eu` (intra community trade, only applicable for accounts in the EU))
- `activity_hours_modified` (shows whether any positions have been modified and do correspond to the timesheet)

```json
{
  "id": 80547,
  "customer_id": 760269602,
  "project_id": 944514545,
  "identifier": "R1704-013",
  "date": "2017-04-05",
  "due_date": "2017-04-25",
  "service_period": "10/2018",
  "service_period_from": "2018-10-01",
  "service_period_to": "2018-10-31",
  "status": "paid",
  "reversed": true,
  "reversal_invoice_id": 80548,
  "reversal": false,
  "reversed_invoice_id": null,
  "title": "Invoice",
  "recipient_address": "Beispiel AG\r\nBeispielstrasse 123\r\n8000 Zürich",
  "currency": "CHF",
  "net_total": 35612.5,
  "tax": 8,
  "vat": { "tax": 8.0, "reverse_charge": false, "intra_eu": false, "active": true, "print_gross_total": true, "notice_tax_exemption": "", "notice_tax_exemption_alt": "" },
  "gross_total": 38461.5,
  "discount": 10,
  "cash_discount": 2.5,
  "cash_discount_days": 5,
  "debit_number": null,
  "credit_number": null,
  "locked": false,
  "activity_hours_modified": false,
  "salutation": "<div>Wir erlauben uns, Ihnen Folgendes in Rechnung zu stellen:</div>",
  "footer": "<div>Zahlbar ohne Abzug innert 20 Tagen.<br><br>Kontoverbindung...<br><br><br>Herzlichen Dank für Ihren Auftrag.</div>",
  "custom_properties": {
    "ext-ref": "3421"
  },
  "tags": ["Postversand"],
  "file_url": "https://data.mocoapp.com/objects...", ⚠️ this link is only available for short time and changes afterwards
  "user": {
    "id": 1234,
    "firstname": "Jane",
    "lastname": "Doe"
  },
  "items": [
    {
      "id": 387469,
      "type": "title",
      "title": "März 2017",
      "description": null,
      "quantity": 0,
      "unit": null,
      "unit_price": 0,
      "net_total": 0
    },
    {
      "id": 387470,
      "type": "item",
      "title": "Allgemeine Arbeiten",
      "description": null,
      "quantity": 15.5,
      "unit": "h",
      "unit_price": 185,
      "net_total": 2867.5
    },
    {
      "id": 387471,
      "type": "item",
      "title": "Umsetzung Backend",
      "description": null,
      "quantity": 4.25,
      "unit": "h",
      "unit_price": 185,
      "net_total": 786.25
    },
    {
      "id": 387472,
      "type": "item",
      "title": "Umsetzung Frontend",
      "description": null,
      "quantity": 110.25,
      "unit": "h",
      "unit_price": 185,
      "net_total": 20396.25
    },
    {
      "id": 387473,
      "type": "item",
      "title": "Hosting Dienstleistungen",
      "description": null,
      "quantity": 45.5,
      "unit": "h",
      "unit_price": 185,
      "net_total": 8417.5
    },
    {
      "id": 387474,
      "type": "item",
      "title": "Support",
      "description": null,
      "quantity": 11.75,
      "unit": "h",
      "unit_price": 185,
      "net_total": 2173.75
    },
    {
      "id": 387475,
      "type": "item",
      "title": "Projektleitung / Kommunikation",
      "description": null,
      "quantity": 5.25,
      "unit:": "h",
      "unit_price": 185,
      "net_total": 971.25
    }
  ],
  "payments": [
    {
      "id": 65938,
      "date": "2017-05-30",
      "paid_total": 10000,
      "currency": "CHF",
      "created_on": "2017-06-05",
      "updated_on": "2017-06-05"
    },
    {
      "id": 65939,
      "date": "2017-07-06",
      "paid_total": 28461.5,
      "currency": "CHF",
      "created_on": "2017-07-10",
      "updated_on": "2017-07-10"
    }
  ],
  "reminders": [
    {
      "id": 2291,
      "date": "2017-05-18",
      "due_date": "2017-05-28",
      "fee": 0,
      "text": "<div>Sehr geehrte Damen und Herren<br><br>Bei der Kontrolle unserer Buchhaltung ist uns aufgefallen ...",
      "created_on": "2017-05-18",
      "updated_on": "2017-05-18"
    }
  ],
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

### Reversal Invoice Fields

- **reversed** – Boolean, when true, the invoice has been reversed (canceled)
- **reversal_invoice_id** – Is only set if the invoice has been reversed and contains the ID of the reversal invoice (cancelation invoice)
- **reversal** – Boolean, when true, the invoice is a reversal invoice (cancelation invoice)
- **reversed_invoice_id** – Is only set if the invoice is a reversal invoice (cancelation invoice) and contains the ID of the reversed invoice (canceled invoice)

## GET /invoices

Retrieve all invoices:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Additionally, these parameters can be supplied:

- [Global filters apply](../entities#global-filters)
- **status** – ("draft", "created", "sent", "partially_paid", "paid", "overdue", "ignored") - multiple values are allowed, comma-separated.
- **include_disregarded** true/false (if "marked as billed" should also be retrieved, default: false)
- **not_booked** – true/false
- **date_from** – "2018-01-01"
- **date_to** – "2018-01-31"
- **service_period_from** – "2018-01-01"
- **service_period_to** – "2018-01-31"
- **tags** "Periodenfremd, Inkasso" (comma separated list)
- **identifier** "R1903-003"
- **term** - "term" (wildcard search within title and identifier)
- **company_id** - 1234
- **project_id** - 5678

The response returns an array with all the invoice information (see attributes), except `salutation`, `footer`, `items`, `payments` and `reminders`.

⚠️ For the status "disregarded," which is not included by default, the response has far fewer fields.

## GET /invoices/locked

Retrieve all locked invoices:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/locked' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Additionally, the following parameters can be supplied:

- **status** – ("draft", "created", "sent", "partially_paid", "paid", "overdue", "ignored")
- **date_from** – "2018-01-01"
- **date_to** – "2018-01-31"
- **identifier** "R1903-003"

The response returns an array with all the invoice information (see attributes), except `salutation`, `footer`, `items`, `payments` and `reminders`.

## GET /invoices/{id}

Retrieve a single invoice:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns a single invoice representation, including internal contact, positions, payments and reminders.

## GET /invoices/{id}.pdf

Retrieve a single invoice document:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}.pdf' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Additionally, the following parameters can be supplied:

- **blank** – (to get the invoice without the letter paper)
- **letter_paper_id** – (the letter paper ID, if left off the default letter paper will be taken)

This returns this invoice's PDF document.

## GET /invoices/{id}/timesheet

Retrieve a time sheet for a particular invoice, i.e. all activities that were invoiced.

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}/timesheet' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns a list of activities:

```json
[
  {
    "id": 988913748,
    "date": "2021-01-25",
    "hours": 4.0,
    "description": "Description",
    "billed": true,
    "billable": true,
    "tag": "",
    "remote_service": "trello",
    "remote_id": "0FhzirkJ",
    "remote_url": "https://trello.com/c/0FhziaBc/1-test",
    "project": {
      "id": 944807389,
      "name": "Pitch Project",
      "billable": true
    },
    "task": {
      "id": 2262446,
      "name": "Design / UX",
      "billable": true
    },
    "customer": {
      "id": 760255659,
      "name": "Acme Corp."
    },
    "user": {
      "id": 933618783,
      "firstname": "Jane",
      "lastname": "Doe"
    },
    "timer_started_at": null,
    "created_at": "2021-02-26T10:48:28Z",
    "updated_at": "2021-02-26T11:42:47Z",
    "hourly_rate": 150.0
  }
]
```

## GET /invoices/{id}/timesheet.pdf

Retrieve a time sheet for a particular invoice:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}/timesheet.pdf' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Additionally, the following parameters can be supplied:

- **letter_paper_id** – (letter paper ID, default: White)

This returns a PDF document or a status code 404, if no hours are available.

## GET /invoices/{id}/expenses

Retrieve all expenses that were invoiced in a particular invoice.

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}/expenses' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns a list of expenses:

```json
[
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
    "recurring_expense_id": null,
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
]
```

## PUT /invoices/{id}/update_status

{: .note }
Only works for actual invoices, not invoice drafts. It's not possible to convert a draft to a regular invoice.

Update an invoice status:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}/update_status' \
  -H 'authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "status": "sent"
      }'
```

The following states are valid: "created", "sent", "overdue", "ignored" – the invoice status is set automatically, as soon as a payment is created.

## POST /invoices

Create an invoice:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/invoices' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "customer_id": 123456,
        "project_id": 654321,
        "recipient_address": "Mein Kunde\nHauptstrasse 1\n8000 Zürich",
        "date": "2018-09-17",
        "due_date": "2018-10-16",
        "title": "Invoice",
        "tax": 8.0,
        "currency": "CHF",
        "service_period_from": "2019-12-01",
        "service_period_to": "2019-12-31",
        "internal_contact_id": 1234,
        "items": [
          {
            "type": "title",
            "title": "Hours"
          },
          {
            "type": "description",
            "description": "Listing of all hours"
          },
          {
            "type": "item",
            "title": "Hosting",
            "quantity": 1,
            "unit": "Stk",
            "unit_price": 99.0
          },
          {
            "type": "separator"
          },
          {
            "type": "item",
            "title": "Design",
            "quantity": 3,
            "unit": "h",
            "unit_price": 150.0
          },
          {
            "type": "item",
            "title": "Setup MailChimp (pauschal)",
            "net_total": 400.00
          }
        ]
    }'
```

Mandatory fields are marked with a star (\*):

- **customer_id\*** – 123456 (ID of the assigned client)
- **recipient_address\*** – "My customer..."
- **date\*** – "2018-09-17"
- **due_date\*** – "2018-10-16"
- **service_period_from** – "2018-08-01"
- **service_period_to** – "2018-08-30"
- **title\*** – "Invoice"
- **tax\*** – 8.0
- **currency\*** – "CHF" (a valid currency of the account)
- **items\*** – positions (see [attributes](#attributes))
- **status** – `created` / `draft` , default is `created`, specify `draft` in order to create a draft invoice
- **change_address** – address propagation ("invoice", "project", "customer"), default is "invoice"
- **salutation** (salutation text)
- **footer** (footer text)
- **discount** – 10 (discount in percent)
- **cash_discount** – 2.5 (cash discount in percent)
- **cash_discount_days** – 5 (cash discount due days)
- **project_id** – 654321 (ID of the assigned project)
- **internal_contact_id** - 1234 (ID of an internal user)
- **custom_properties** – {"ext-ref": "5433"}
- **tags** – ["Hosting", "Europe"]
- **print_detail_columns**  - true (Hide/Display 'quantity, unit, price'). Optional property, which defaults to the global account layout setting

Omitted fields `service_period_from` and `service_period_to` indicates the absences of a service period.

Items with `quantity`, `unit` and `unit_price` can be used to select activities or expenses to be billed by this invoice,
just specify the IDs using respectively `activity_ids` and `expense_ids`, for example:

```json
{
  "type": "item",
  "title": "Design",
  "quantity": 3,
  "unit": "h",
  "unit_price": 150.0,
  "activity_ids": [1253, 8712]
}
```

### Variables

It's possible to use variables in the salutation and footer texts. Use curly braces like `{variable}` to use them:

* `{salutation}`
* `{date}`
* `{due_date}`
* `{due_days}`
* `{recipient}` - full address
* `{company_name}`
* `{net_total}`
* `{tax}`
* `{gross_total}`
* `{title}`
* `{identifier}` - invoice number
* `{me}` - current user full name
* `{me_firstname}`
* `{me_email}`
* `{me_details}` - full name, email, phone number
* `{user}` - invoice creator full name 
* `{user_email}` 
* `{user_details}` - invoice creator full name, email, phone number
* `{internal_contact}`
* `{internal_contact_email}`
* `{internal_contact_details}`
* `{service_period}`
* `{cash_discount}`
* `{cash_discount_days}`
* `{cash_discount_total}`
* `{gross_total_with_cash_discount}`
* `{signature_image}` - email signature image

## POST /invoices/{id}/send_email

Send the invoice by email:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}/send_email' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "emails_to": "somebody@example.com",
        "subject": "Invoice",
        "text": "Kind regards"
      }'
```

Mandatory fields are marked with a star (\*):

- **subject\*** – "Invoice",
- **text\*** – "Kind regards"
- **emails_to** – "somebody@example.com;info@example.com" (list of addresses separated by _;_). To use default recipients, see information below.
- **emails_cc** – "somebodyelse@example.com" (list of addresses separated by _;_)
- **emails_bcc** – "somebody@partner.example.com" (list of addresses separated by _;_)
- **letter_paper_id** – 123 (the letter paper ID to use, leave blank for the default letter paper)

🛈 If you want to send emails to the default recipients configured in the project or on the customer, leave `emails_to`, `emails_cc` and `emails_bcc` empty. `emails_to` always needs to be provided, either via the default recipients or as a given value. In the response, the recipients selected are returned.

## DELETE /invoices/{id}

Delete a single invoice:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
  -H 'Content-Type: application/json' \
  -d '{
        "reason": "Wrong invoice number",
      }'
```

Mandatory fields are marked with a star (\*):

- **reason\*** – "Wrong invoice number" (a reason why this invoice is being deleted), This can only be omitted if the invoice to be deleted is a draft.

## GET /invoices/{id}/attachments

List all attachments for this invoice:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/{invoice_id}/attachments' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Provide the payload base64 encoded.

## POST /invoices/{invoice_id}/attachments

Add attachment PDF to invoice:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/invoices/{invoice_id}/attachments' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "attachment": {
          "filename": "attachment.pdf",
          "base64": "JVBERi0xLjQKJeLjz9MKNCAwIG9iago8PC9GaWx..."
        }
      }'
```

Provide the payload base64 encoded.

## DELETE /invoices/{invoice_id}/attachments/{id}

Remove attachment from invoice:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/invoices/{invoice_id}/attachments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
