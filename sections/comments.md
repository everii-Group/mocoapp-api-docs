# Comments
German: "Notizen"

## Attributes

The representation contains, among the standard fields, also:

* user (creator)

```json
{
    "id": 123,
    "commentable_id": 12345,
    "commentable_type": "Project",
    "text": "Project was ordered on 1.10.2017.",
    "manual": true,
    "created_at": "2018-10-17 09:33:46 +0100",
    "updated_at": "2018-10-17 09:33:46 +0100",
    "user": {
        "id": 567,
        "firstname": "Tobias",
        "lastname": "Miesel"
    }
}
```

## GET /comments

Retrieve all comments

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/comments' \
  -H 'Authorization: Token token={api-key}'
```

This returns complete comment information (see Attributes).

Additionally, the following parameters can be supplied:

* **commentable_type** – "User", "Deal", "Offer", "OfferConfirmation", "Customer", "Project", "Invoice", "Contact" (object this comment relates to)
* **commentable_id** – 123 (object ID)
* **user_id** – 456 (creator user ID)
* **manual** – true/false (user-created or generated)

## GET /comments/{id}

Retrieve a single comment:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/comments/{id}' \
  -H 'Authorization: Token token={api-key}'
```

This returns a single comment representation.

## POST /comments

Create a comment:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/comments' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "commentable_id": 123,
        "commentable_type": "Project",
        "text": "Project was ordered."
      }'
```

Mandatory fields are marked with a star (*):

* **commentable_id*** – 123 (object ID)
* **commentable_type*** – "User", "Deal", "Offer", "OfferConfirmation", "Customer", "Project", "Invoice", "Contact" (object type)
* **text*** – "Comment text..."

## PUT /comments/{id}

Update a comment:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/comments/{id}' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "text": "Project is paused for now.",
      }'
```

Fields are analogous to the POST request.

## DELETE /comments/{id}

Deleting manually created comments:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/comments/{id}' \
  -H 'Authorization: Token token={api-key}'
```
