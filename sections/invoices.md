# Invoices
German: "Rechnungen"

## Attributes

The invoice representation contains among standard fields also:

* positions (items)
* position types ("title", "description", "item", "subtotal", "page-break" or "separator")
* payments
* reminders

```json
{
    "id": 80547,
    "customer_id": 760269602,
    "project_id": 944514545,
    "identifier": "R1704-013",
    "date": "2017-04-05",
    "due_date": "2017-04-25",
    "status": "paid",
    "reversal": false,
    "title": "Invoice",
    "recipient_address": "Beispiel AG\r\nBeispielstrasse 123\r\n8000 Zürich",
    "currency": "CHF",
    "net_total": 35612.5,
    "tax": 8,
    "gross_total": 38461.5,
    "created_on": "2017-04-04",
    "updated_on": "2017-07-10",
    "debit_number": null,
    "credit_number": null,
    "locked": false,
    "salutation": "<div>Wir erlauben uns, Ihnen Folgendes in Rechnung zu stellen:</div>",
    "footer": "<div>Zahlbar ohne Abzug innert 20 Tagen.<br><br>Kontoverbindung...<br><br><br>Herzlichen Dank für Ihren Auftrag.</div>",
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
            "unit": "h",
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
            "salutation": "<div>Sehr geehrte Damen und Herren<br><br>Bei der Kontrolle unserer Buchhaltung ist uns aufgefallen, dass wir für folgende Rechnung noch keinen Zahlungseingang verbuchen konnten:</div>",
            "footer": "<div>Sicherlich handelt es sich hierbei um ein Versehen. Wir bitten Sie höflich, uns den Betrag in den nächsten Tagen auf unser Bankkonto zu überweisen. Sollte sich Ihre Zahlung mit diesem Schreiben gekreuzt haben, betrachten Sie diese Erinnerung als gegenstandslos.<br><br>Kontoverbindung:&nbsp;<br>Zürcher Kantonalbank<br>IBAN: CH00 0000 0000 0000 0000 0.<br><br>Herzlichen Dank.</div>",
            "created_on": "2017-05-18",
            "updated_on": "2017-05-18"
        }
    ]
}
```

## GET /invoices

Retrieve all invoices:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices' \
  -H 'Authorization: Token token={api-key}'
```

Additionally, these parameters can be supplied:

* **status** – ("draft", "created", "sent", "partially_paid", "paid", "overdue", "ignored")
* **date_from** – "2018-01-01"
* **date_to** – "2018-01-31"

The response returns an array with all the invoice information (see attributes), except `salutation`, `footer`, `items`, `payments` and `reminders`.

## GET /invoices/locked

Retrieve all locked invoices:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/locked' \
  -H 'Authorization: Token token={api-key}'
```

Additionally, the following parameters can be supplied:

* **status** – ("draft", "created", "sent", "partially_paid", "paid", "overdue", "ignored")
* **date_from** – "2018-01-01"
* **date_to** – "2018-01-31"

The response returns an array with all the invoice information (see attributes), except `salutation`, `footer`, `items`, `payments` and `reminders`.

## GET /invoices/{id}

Retrieve a single invoice:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}' \
  -H 'Authorization: Token token={api-key}'
```

This returns a single invoice representation, including positions, payments and reminders.

## GET /invoices/{id}.pdf

Retrieve a single invoice document:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}.pdf' \
  -H 'Authorization: Token token={api-key}'
```

Additionally, the following parameters can be supplied:

* **letter_paper_id** – (letter paper ID, default: White)

This returns this invoice's PDF document.

## GET /invoices/{id}/timesheet.pdf

Retrieve a time sheet for a particular invoice:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}/timesheet.pdf' \
  -H 'Authorization: Token token={api-key}'
```

Additionally, the following parameters can be supplied:

* **letter_paper_id** – (letter paper ID, default: White)

This returns a PDF document or a status code 404, if no hours are available.

## PUT /invoices/{id}/update_status

Update an invoice status:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/invoices/{id}/update_status' \
  -H 'authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "status": "sent"
      }'
```

The following states are valid: "created", "sent", "overdue", "ignored" – the invoice status is set automatically, as soon as a payment is created.

## POST /invoices

Create a neutral invoice:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/invoices' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "customer_id": 123456,
        "project_id": 654321,
        "recipient_address": "Mein Kunde\nHauptstrasse 1\n8000 Zürich",
        "change_address": "invoice",
        "date": "2018-09-17",
        "due_date": "2018-10-16",
        "title": "Invoice",
        "salutation": "",
        "tax": 8.0,
        "discount": 0.0,
        "currency": "CHF",
        "footer": "",
        "service_period": "Aug 18",
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
            "type": "seperator"
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

Mandatory fields are marked with a star (*):

* **customer_id*** – 123456
* **project_id*** – 654321 (ID of the assigned project)
* **recipient_address*** – "My customer..."
* **change_address*** – Take over this address ("invoice", "project", "customer")
* **date*** – "2018-09-17"
* **due_date*** – "2018-10-16"
* **title*** – "Invoice"
* **salutation***– ""
* **tax*** – 8.0
* **discount*** – 0.0
* **hours*** – 1.0
* **currency*** – 1.0
* **footer***– ""
* **service_period***– "Aug 18"
* **items** – positions (see Attributes)
