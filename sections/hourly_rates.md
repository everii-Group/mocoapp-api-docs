# Hourly Rates

German: "Stundensätze"

## GET /hourly_rates

Retrieve hourly rates:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/hourly_rates' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

The following parameters can be supplied:

- **company_id** – 123456 (if overwritten: customer hourly rates, if not: global hourly rates)

### Response

```json
{
  "defaults_rates": [
    { "currency": "CHF", "hourly_rate": 160.0 },
    { "currency": "EUR", "hourly_rate": 150.0 },
    { "currency": "USD", "hourly_rate": 160.0 }
  ],
  "tasks": [
    {
      "id": 5004,
      "name": "Grafik",
      "rates": [
        { "currency": "CHF", "hourly_rate": 160.0 },
        { "currency": "EUR", "hourly_rate": 150.0 },
        { "currency": "USD", "hourly_rate": 160.0 }
      ]
    },
    {
      "id": 5005,
      "name": "Entwicklung",
      "rates": [
        { "currency": "CHF", "hourly_rate": 160.0 },
        { "currency": "EUR", "hourly_rate": 150.0 },
        { "currency": "USD", "hourly_rate": 160.0 }
      ]
    },
    {
      "id": 5006,
      "name": "Projektleitung",
      "rates": [
        { "currency": "CHF", "hourly_rate": 170.0 },
        { "currency": "EUR", "hourly_rate": 160.0 },
        { "currency": "USD", "hourly_rate": 170.0 }
      ]
    }
  ],
  "users": [
    {
      "id": 933589840,
      "full_name": "Max Muster",
      "rates": [
        { "currency": "CHF", "hourly_rate": 160.0 },
        { "currency": "EUR", "hourly_rate": 150.0 },
        { "currency": "USD", "hourly_rate": 160.0 }
      ]
    },
    {
      "id": 933589844,
      "full_name": "Peter Müller",
      "rates": [
        { "currency": "CHF", "hourly_rate": 180.0 },
        { "currency": "EUR", "hourly_rate": 170.0 },
        { "currency": "USD", "hourly_rate": 180.0 }
      ]
    }
  ]
}
```
