# Deal Categories

German: "Akquise-Stufen"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /deal_categories](#get-deal_categories)
- [GET /deal_categories/{id}](#get-deal_categoriesid)
- [POST /deal_categories](#post-deal_categories)
- [PUT /deal_categories/{id}](#put-deal_categoriesid)
- [DELETE /deal_categories/{id}](#delete-deal_categoriesid)

<!-- /TOC -->

## Attributes

The deal category representation is:

```json
{
  "id": 123,
  "name": "Contact",
  "probability": 1,
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /deal_categories

Retrieve all categories:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/deal_categories' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete category information (see attributes).

Additionally, the following parameters can be supplied:

- **ids** – e.g. `123,456` (IDS, comma-separated)

## GET /deal_categories/{id}

Retrieve a single category:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/deal_categories/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

The response is a single category representation.

## POST /deal_categories

Create a category:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/deal_categories' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "New Category",
        "probability": 15,
      }'
```

Mandatory fields are marked with a star (\*):

- **name\*** – "New Category"
- **probability\*** – 15

## PUT /deal_categories/{id}

Update a category:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/deal_categories/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "New Name"
      }'
```

Fields are analogous to the POST request.

## DELETE /deal_categories/{id}

Delete a category.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/deal_categories/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Response code is _no-content_ on success.
If the category is in use then the delete fails and response code is _forbidden_.
