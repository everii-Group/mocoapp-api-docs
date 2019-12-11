# Companies

German: "Firmen"

## Attributes

The company representation contains among default fields the following features:

- Type ("customer", "supplier", "organization")
- Labels
- Custom properties
- Projects (shortened)
- User (shortened)

```json5
{
  id: 760253573,
  type: "customer",
  name: "Beispiel AG",
  website: "www.beispiel-ag.com",
  email: "info@beispiel-ag.com",
  phone: "+49 30 123 45 67",
  fax: "+49 30 123 45 66",
  address: "Beispiel AG\nBeispielstrasse 123\n12345 Beispielstadt",
  tags: ["Netzwerk", "Druckerei"],
  user: {
    id: 933589840,
    firstname: "Tobias",
    lastname: "Miesel"
  },
  labels: ["Netzwerk", "Druckerei"], // 🚧 DEPRECATED: use tags
  info: "",
  custom_properties: {
    UID: "1234-UID-4567"
  },
  identifier: "36",
  intern: false,
  billing_tax: 0,
  currency: "CHF",
  country_code: "CH",
  default_invoice_due_days: 30,
  footer: "<div>Footer text</div>", // appears at the end of invoices
  projects: [
    {
      id: 944504145,
      identifier: "46",
      name: "Layoutanpassung",
      active: false,
      billable: true
    }
  ],
  created_at: "2018-10-17T09:33:46Z",
  updated_at: "2018-10-17T09:33:46Z"
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

- **type** ("customer", "supplier", "organization")
- **tags** "Automotive, Pharma" (comma separated list)
- **identifier** "K0405"

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
- **website** – "http//www.lieferant.com"
- **fax** – "+49 30 123 45 67"
- **phone** – "+49 30 123 45 67"
- **email** – "bestellung@lieferant.de"
- **address** – "Lieferant AG\nBeispielstrasse 123\n12345 Berlin"
- **info** – "Information for this company..."
- **custom_properties** – {"UID": "123-UID-456"}
- **labels** – ["Network", "Print"] 💡name mismatch, labels/tags are used interchangeably
- **user_id** – 123456 💡(responsible person)
- **footer** – "<div>some html</div>" (appears at the end of invoices)

Additional fields just for companies of type customer:

- **currency\*** – "EUR"
- **identifier\*** – "K-123" (only mandatory if not automatically assigned)
- **billing_tax** – 19.0
- **default_invoice_due_days** – 20

## PUT /companies/{id}

Update a company.

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/companies/{123}' \
  -H 'authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Beispiel GmbH",
      }'
```

Fields are analogous to the POST request.

## DELETE /companies/{id}

⚠ Deleting a company is not possible via API!
