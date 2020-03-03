# Purchase Categories

German: "Ausgaben – Kategorien"

## Attributes

The purchase category representation is:

```json5
{
  "id": 123,
  "name": "Travel expenses",
  "credit_account": "6640",
  "active": true,
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /purchases/categories

Retrieve all categories:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases/categories' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete category information (see attributes).

## GET /purchases/categories/{id}

Retrieve a single category:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/purchases/categories/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

The response is a single category representation.
