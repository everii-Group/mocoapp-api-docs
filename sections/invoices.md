# Invoices

German: "Rechnungen"

<!-- TOC depthfrom:2 -->

- [Attributes](#attributes)
- [GET /invoices](#get-invoices)
- [GET /invoices/locked](#get-invoiceslocked)
- [GET /invoices/{id}](#get-invoicesid)
- [GET /invoices/{id}.pdf](#get-invoicesidpdf)
- [GET /invoices/{id}/timesheet](#get-invoicesidtimesheet)
- [GET /invoices/{id}/timesheet.pdf](#get-invoicesidtimesheetpdf)
- [PUT /invoices/{id}/update_status](#put-invoicesidupdate_status)
- [POST /invoices](#post-invoices)
- [POST /invoices/{id}/send_email](#post-invoicesidsend_email)
- [DELETE /invoices/{id}](#delete-invoicesid)

<!-- /TOC -->

## Attributes

The invoice representation contains among standard fields also:

- custom properties
- positions (items)
- position types ("title", "description", "item", "subtotal", "page-break" or "separator")
- payments
- reminders
- vat ("tax", "reverse_charge", "intra_eu" (intra community trade, only applicable for accounts in the EU))

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
  "vat": { "tax": 8.0, "reverse_charge": false, "intra_eu": false },
  "gross_total": 38461.5,
  "discount": 10,
  "cash_discount": 2.5,
  "cash_discount_days": 5,
  "debit_number": null,
  "credit_number": null,
  "locked": false,
  "salutation": "<div>Wir erlauben uns, Ihnen Folgendes in Rechnung zu stellen:</div>",
  "footer": "<div>Zahlbar ohne Abzug innert 20 Tagen.<br><br>Kontoverbindung...<br><br><br>Herzlichen Dank für Ihren Auftrag.</div>",
  "custom_properties": {
    "ext-ref": "3421"
  },
  "tags": ["Postversand"],
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

- **status** – ("draft", "created", "sent", "partially_paid", "paid", "overdue", "ignored")
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
      "firstname": "Doe",
      "lastname": "Jane"
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

## PUT /invoices/{id}/update_status

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
- **status** – `created`|`draft` , default is `created`, specify `draft` in order to create a draft invoice
- **change_address** – address propagation ("invoice", "project", "customer"), default is "invoice"
- **salutation** (salutation text)
- **footer** (footer text)
- **discount** – 10 (discount in percent)
- **cash_discount** – 2.5 (cash discount in percent)
- **cash_discount_days** – 5 (cash discount due days)
- **project_id** – 654321 (ID of the assigned project)
- **custom_properties** – {"ext-ref": "5433"}
- **tags** – ["Hosting", "Europe"]

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
