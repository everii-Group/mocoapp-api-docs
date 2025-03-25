---
layout: default
parent: Entities
---

# Companies

German: "Firmen"

- TOC
{:toc}

## Attributes

The company representation contains among default fields the following features:

- Type ("customer", "supplier", "organization")
- Tags
- Custom properties
- Projects (shortened)
- User (shortened)
- billing_vat ("tax", "reverse_charge", "intra_eu" (intra community trade, only applicable for accounts in the EU))

```json
{
  "id": 760253573,
  "type": "customer",
  "name": "Beispiel AG",
  "website": "www.beispiel-ag.com",
  "email": "info@beispiel-ag.com",
  "billing_email_cc": "cc@beispiel-ag.com",
  "phone": "+49 30 123 45 67",
  "fax": "+49 30 123 45 66",
  "address": "Beispiel AG\nBeispielstrasse 123\n12345 Beispielstadt",
  "tags": ["Netzwerk", "Druckerei"],
  "user": {
    "id": 933589840,
    "firstname": "Tobias",
    "lastname": "Miesel"
  },
  "info": "",
  "custom_properties": {
    "UID": "1234-UID-4567"
  },
  "identifier": "36",
  "intern": false,
  "billing_tax": 0,
  "customer_vat": { "tax": 0.0, "reverse_charge": true, "intra_eu": true, "active": true, "print_gross_total": true, "notice_tax_exemption": "", "notice_tax_exemption_alt": "" }, // for customers only
  "supplier_vat": { "tax": 0.0, "reverse_charge": true, "intra_eu": true, "active": true }, // for suppliers only
  "currency": "CHF",
  "custom_rates": false,
  "include_time_report": false,
  "billing_notes": "Vor Rechnungsstellung PO beantragen.",
  "default_discount": 0.0,
  "default_cash_discount": 2.0,
  "default_cash_discount_days": 10,
  "country_code": "CH",
  "vat_identifier": "CH999999999",
  "alternative_correspondence_language": false,
  "default_invoice_due_days": 30,
  "footer": "<div>Footer text</div>",
  "projects": [
    {
      "id": 944504145,
      "identifier": "46",
      "name": "Layoutanpassung",
      "active": false,
      "billable": true
    }
  ],
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z",
  "debit_number": 10000
}
```

## GET /companies

Retrieve all companies:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/companies' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's also possible to filter:

{: .note }
To filter by custom properties, you have to supply the `type` parameter.

- [Global filters apply](../entities#global-filters)
- **type** ("customer", "supplier", "organization")
- **tags** "Automotive, Pharma" (comma separated list)
- **identifier** "K0405"
- **term** "acme corp" (search term)

This returns an array with the complete company information.

## GET /companies/{id}

Retrieve a single company:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/companies/123' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns a single company's complete represenation.

## POST /companies

Create a company:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/companies' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Beispiel AG",
        "currency": "EUR"
      }'
```

Fields for all types of companies. Mandatory fields are marked with a star (\*):

- **name\*** – "Beispiel AG"
- **type\*** – ("customer", "supplier", "organization")
- **country_code** – (ISO Alpha-2 Country Code like "DE" / "CH" / "AT" in upper case - default is account country)
- **vat_identifier** – European Union VAT identification numbers (USt-IdNr)
- **alternative_correspondence_language** – true/false (create sales documents in the account alternative language)
- **website** – "http//www.lieferant.com"
- **fax** – "+49 30 123 45 67"
- **phone** – "+49 30 123 45 67"
- **email** – "bestellung@lieferant.de"
- **billing_email_cc** - "cc@lieferant.de"
- **billing_notes** - "Rechnung mit Stundenauszug schicken"
- **address** – "Lieferant AG\nBeispielstrasse 123\n12345 Berlin"
- **info** – "Information for this company..."
- **custom_properties** – {"UID": "123-UID-456"}
- **tags** – ["Network", "Print"]
- **user_id** – 123456 💡(responsible person)
- **footer** – "<div>some html</div>" (appears at the end of invoices)

Additional fields just for companies of type customer:

- **currency\*** – "EUR"
- **identifier\*** – "K-123" (only mandatory if not automatically assigned)
- **customer_tax** – 19.0
- **default_invoice_due_days** – 20 (use **invoice_due_days** to set a value for a company)
- **debit_number** – 10000 if bookkeeping is enabled

Additional fields just for companies of type supplier:

- **iban** – CH3908704016075473007
- **supplier_tax** – 19.0
- **credit_number** – 70000 if bookkeeping is enabled

## PUT /companies/{id}

Update a company.

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/companies/{123}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Beispiel GmbH"
      }'
```

Fields are analogous to the POST request.

## DELETE /companies/{id}

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/companies/{123}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
