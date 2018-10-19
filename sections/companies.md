# Companies
German: "Firmen"


## Attributes

The company representation contains among default fields the following features:

* Type ("customer", "supplier", "organization")
* Labels
* Custom properties
* Projects (shortened)

```json
{
    "id": 760253573,
    "type": "customer",
    "name": "Beispiel AG",
    "website": "www.beispiel-ag.com",
    "email": "info@beispiel-ag.com",
    "phone": "+49 30 123 45 67",
    "fax": "+49 30 123 45 66",
    "address": "Beispiel AG\nBeispielstrasse 123\n12345 Beispielstadt",
    "labels": ["Netzwerk", "Druckerei"],
    "info": "",
    "custom_properties": {
        "UID": "1234-UID-4567"
    },
    "identifier": "36",
    "intern": false,
    "billing_tax": 0,
    "currency": "CHF",
    "default_invoice_due_days": 30,
    "projects": [
        {
            "id": 944504145,
            "identifier": "46",
            "name": "Layoutanpassung",
            "active": false,
            "billable": true
        }
    ]
}
```

## GET /companies

Retrieve all companies:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/companies' \
  -H 'Authorization: Token token={api-key}'
```

It's also possible to filter by type:

* **type** ("customer", "supplier", "organization")

This returns an array with the complete company information.

## GET /companies/{id}

Retrieve a single company:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/companies/123' \
  -H 'Authorization: Token token={api-key}'
```

This returns a single company's complete represenation.

## POST /companies

Create a company:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/companies' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Beispiel AG",
        "currency": "EUR"
      }'
```

Fields for all types of companies. Mandatory fields are marked with a star (*):

* **name*** – "Beispiel AG"
* **type*** – ("customer", "supplier", "organization")
* **website** – "http//www.lieferant.com"
* **fax** – "+49 30 123 45 67"
* **phone** – "+49 30 123 45 67"
* **email** – "bestellung@lieferant.de"
* **address** – "Lieferant AG\nBeispielstrasse 123\n12345 Berlin"
* **info** – "Information for this company..."
* **custom_properties** – {"UID": "123-UID-456"}
* **labels** – ["Network", "Print"]


Additional fields just for companies of type customer:

* **currency*** – "EUR"
* **identifier*** – "K-123" (only mandatory if not automatically assigned)
* **billing_tax** – 19.0
* **default_invoice_due_days** – 20

## PUT /companies/{id}

Update a company.

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/companies/{123}' \
  -H 'authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Beispiel GmbH",
      }'
```

Fields are analogous to the POST request.

## DELETE /companies/{id}

⚠ Deleting a company is not possible via API!
