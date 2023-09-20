---
layout: default
parent: Entities
---

# Offers

German: "Angebote"

- TOC
{:toc}

## Attributes

The offer representation contains among the standard fields:

- custom properties
- positions (items)
- position types ("title", "description", "item", "subtotal", "page-break" or "separator")
- vat ("tax", "reverse_charge", "intra_eu" (intra community trade, only applicable for accounts in the EU))

```json
{
  "id": 273,
  "identifier": "A1704-042",
  "date": "2017-04-12",
  "due_date": "2017-04-26",
  "title": "Offer - User Management",
  "recipient_address": "Beispiel GmbH\nPeter Muster\nBeispielstrasse 123\n12345 Berlin",
  "currency": "EUR",
  "net_total": 12750,
  "tax": 19,
  "vat": { "tax": 19.0, "reverse_charge": false, "intra_eu": false },
  "gross_total": 15172.5,
  "discount": 10,
  "salutation": "Hallo Peter<br><br>Folgende Aufwände schätzen wir für die Umsetzung der Komponenten:",
  "footer": "Für Rückfragen stehe ich dir jederzeit gerne zur Verfügung.<br><br>Viele Grüsse<br><br>Tobias",
  "tags": ["Print", "Digital"],
  "custom_properties": {
    "ext-ref": "3421"
  },
  "company": {
    "id": 1234,
    "name": "Acme Corp."
  },
  "project": {
    "id": 1234,
    "name": "A Project"
  },
  "deal": {
    "id": 1234,
    "name": "A Lead"
  },
  "user": {
    "id": 1234,
    "firstname": "Jane",
    "lastname": "Doe"
  },
  "offer_confirmation": {
    "id": 1234,
    "title": "Offer confirmation",
    "created_at": "2022-12-12T09:33:46Z",
    "updated_at": "2022-12-12T09:33:46Z"
  },
  "items": [
    {
      "id": 29,
      "type": "item",
      "title": "Project Setup",
      "description": null,
      "quantity": 1,
      "unit": "d",
      "unit_price": 1500,
      "net_total": 1500,
      "optional": false
    },
    {
      "id": 30,
      "type": "item",
      "title": "Master Data",
      "description": null,
      "quantity": 3,
      "unit": "d",
      "unit_price": 1500,
      "net_total": 4500,
      "optional": false
    },
    {
      "id": 31,
      "type": "description",
      "title": null,
      "description": "Master data can be added.",
      "quantity": 0,
      "unit": null,
      "unit_price": 0,
      "net_total": 0,
      "optional": false
    },
    {
      "id": 34,
      "type": "item",
      "title": "OAuth Provider (Single Sign On)",
      "description": null,
      "quantity": 4,
      "unit": "d",
      "unit_price": 1500,
      "net_total": 6000,
      "optional": false
    },
    {
      "id": 35,
      "type": "description",
      "title": null,
      "description": "This component runs centrally and provides an OAuth Provider.<br>Other applications can access this authorization service.",
      "quantity": 0,
      "unit": null,
      "unit_price": 0,
      "net_total": 0,
      "optional": false
    },
    {
      "id": 38,
      "type": "item",
      "title": "Project Management / Communication / Hand-Over",
      "description": null,
      "quantity": 0.5,
      "unit": "d",
      "unit_price": 1500,
      "net_total": 750,
      "optional": false
    }
  ],
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /offers

Retrieve all offers:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/offers' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete offer information (see Attributes), except: `salutation`, `footer` and `items`.

Offers can be sorted by: `date`, `created_at` and `title`:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/offers?sort=date' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Additionally, these parameters can be supplied:

- [Global filters apply](../entities#global-filters)
- **status** – ("created", "sent", "accepted", "partially_billed", "billed", "archived")
- **from** – "2018-01-01"
- **to** – "2018-01-31"
- **identifier** – "A1903-003"
- **deal_id** – "123,456" (deal ID for offers on this deal, single or comma-separated values)
- **project_id** – "123,456" (project ID for offers on this project, single or comma-separated values)

## GET /offers/{id}

Retrieve a single offer:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/offers/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns a single offer representation, including internal contact and positions.

## GET /offers/{id}.pdf

Retrieve a single offer document:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/offers/{id}.pdf' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Additionally, the following parameters can be supplied:

- **letter_paper_id** – (letter paper ID, default: White)

This returns this offers's PDF document.

## POST /offers

Create an offer:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/offers' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "deal_id": 123,
        "recipient_address": "Acme\r\nPark Avenue",
        "date": "2019-05-10",
        "due_date": "2019-06-08",
        "title": "Offer - Shop Locator",
        "salutation": "Hey",
        "tax": 8.0,
        "discount": 0.0,
        "footer": "Bye",
        "internal_contact_id": 1234,
        "items":[
            {"type":"title","title":"Stunden"},
            {"type":"description","description":"Aufstellung über geleistete Arbeiten"},
            {"type":"item","title":"MailChimp Einrichtung","quantity":1,"unit":"Std","unit_price":100.0}
            ]}'
```

Mandatory fields are marked with a star (\*):

{: .warning }
Either `company_id`, `deal_id` or `project_id` have to be provided

- **company_id** – 123456 (ID of the associated company), is disregarded and set to the company of the project if project_id is provided
- **deal_id** – 123456 (ID of the associated deal)
- **project_id** – 123456 (ID of the associated project)
- **recipient_address\*** – "My customer..."
- **date\*** – "2018-09-17"
- **due_date\*** – "2018-10-16"
- **title\*** – "Offer"
- **tax\*** – 8.0
- **currency\*** – "CHF" (a valid currency of the account), must match the currency of provided project and deal, only required if no company_id, deal_id and project_id is provided
- **items\*** – positions (see [attributes](#attributes))
- **change_address** – address propagation ("offer", "customer"), default is "offer"
- **salutation** (salutation text)
- **footer** (footer text)
- **discount** – 10 (discount in percent)
- **contact_id** – 123456 (ID of the associated contact at customer)
- **internal_contact_id** - 1234 (ID of an internal user)
- **tags** – ["Retail"]
- **custom_properties** – {"ext-ref": "3421"}

## PUT /offers/{id}/update_status

Update an offer status:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/offers/{id}/update_status' \
  -H 'authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "status": "billed"
      }'
```

The following states are valid: "created", "sent", "accepted", "partially_billed", "billed", "archived".

## POST /offers/{id}/send_email

Send the offer by email:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/offers/{id}/send_email' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "emails_to": "somebody@example.com",
        "subject": "Offer",
        "text": "Kind regards"
      }'
```

Mandatory fields are marked with a star (\*):

- **subject\*** – "Offer",
- **text\*** – "Kind regards"
- **emails_to** – "somebody@example.com;info@example.com" (list of addresses separated by _;_). To use default recipients, see information below.
- **emails_cc** – "somebodyelse@example.com" (list of addresses separated by _;_)
- **emails_bcc** – "somebody@partner.example.com" (list of addresses separated by _;_)

🛈 If you want to send emails to the default recipients configured on the customer or set as a contact, leave `emails_to`, `emails_cc` and `emails_bcc` empty. `emails_to` always needs to be provided, either via the default recipients or as a given value. In the response, the recipients selected are returned.

## GET /offers/{id}/attachments

List all attachments for this offer:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/offers/{offer_id}/attachments' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Provide the payload base64 encoded.

## POST /offers/{id}/attachments

Add attachment PDF to offer:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/offers/{id}/attachments' \
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

## DELETE /offers/{offer_id}/attachments/{id}

Remove attachment from offer:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/offers/{offer_id}/attachments/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'