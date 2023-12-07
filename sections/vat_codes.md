---
layout: default
parent: Entities
---

# VAT Codes

German: "Steuerschlüssel"

- TOC
{:toc}

## Attributes

### VatCode Sale

```json
{
  "id": 186,
  "tax": 7.7,
  "reverse_charge": false,
  "intra_eu": false,
  "active": true,
  "print_gross_total": true,
  "notice_tax_exemption": "",
  "notice_tax_exemption_en": "",
  "code": "9",
  "credit_account: "4000"
}
```

### VatCode Purchase

```json
{
  "id": 186,
  "tax": 7.7,
  "reverse_charge": false,
  "intra_eu": false,
  "active": true,
  "code": "9"
}
```

## GET /vat_code_sales

Retrieve the list of sale vat codes:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/vat_code_sales' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with sale vat codes (see Attributes).

The following parameters can be supplied to filter sale vat codes:

- [Global filters apply](../entities#global-filters)
- **reverse_charge** – true/false (Umkehr Steuerschuldnerschaft)
- **intra_eu** – true/false (Innergemeinschaftliche Leistung)
- **active** – true/false

## GET /vat_code_purchases

Retrieve the list of purchase vat codes:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/vat_code_purchases' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with purchase vat codes (see Attributes).

The following parameters can be supplied to filter purchase vat codes:

- **ids** – e.g. `123,456` (IDS, comma-separated)
- **reverse_charge** – true/false (Umkehr Steuerschuldnerschaft)
- **intra_eu** – true/false (Innergemeinschaftliche Leistung)
- **active** – true/false

## GET /vat_code_sales/{id}

Retrieve a single sale vat code:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/vat_code_sales/123' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Retrieve a single sale vat code.

## GET /vat_code_purchases/{id}

Retrieve a single purchase vat code:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/vat_code_purchases/123' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Retrieve a single purchase vat code.
