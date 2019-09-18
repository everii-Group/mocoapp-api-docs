# Web Hooks

## Attributes

```json
{
  "id": 123,
  "target": "Activity",
  "event": "create",
  "hook": "https://example.org/do-stuff",
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /accounts/web_hooks

Retrieve all web hooks:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/accounts/web_hooks' \
  -H 'Authorization: Token token={api-key}'
```

This returns an array with complete web hooks information (see Attributes).

## GET /accounts/web_hooks/{id}

Retrieve a single web hook:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/accounts/web_hook/{id}' \
  -H 'Authorization: Token token={api-key}'
```

This returns a single web hook representation.

## POST /accounts/web_hooks

Create a new web hook:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/accounts/web_hooks' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "target": "Activity",
        "event": "create",
        "hook": "https://example.org/do-stuff",
      }'
```

Mandatory fields are marked with a star (\*):

- **target\*** – "Activity" (Activity/Company/Contact/Project/Invoice/Offer/Deal)
- **event\*** – "create" (create/update/delete)
- **hook\*** – "https://example.org/do-stuff" 
- **disabled_at** – "2019-09-01T00:00:00Z", to disable the web hook

## PUT /accounts/web_hooks/{id}

Update the web hook:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/accounts/web_hooks/{id}' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "disabled_at": "2019-09-01T00:00:00Z",
      }'
```

Fiels are analogous to the POST request.

## DELETE /accounts/web_hooks/{id}

Removes the web hook:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/accounts/web_hooks/{id}' \
  -H 'Authorization: Token token={api-key}'
```
