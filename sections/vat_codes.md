# VAT Codes

German: "Steuerschlüssel"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /vat_codes](#get-vat_codes)

<!-- /TOC -->

## Attributes

```json
{
  "id": 186,
  "tax": 7.7,
  "reverse_charge": false,
  "intra_eu": false,
  "kind": "purchase",
  "active": true
}
```

## GET /vat_codes

Retrieve the list of vat codes:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/vat_codes'
```

This returns an array with vat codes (see Attributes).

The following parameters can be supplied:

- **kind** – purchase/invoice (Vorsteuer/Umsatzsteuer)
- **reverse_charge** – true/false (Umkehr Steuerschuldnerschaft)
- **intra_eu** – true/false (Innergemeinschaftliche Leistung)
- **active** – true/false
