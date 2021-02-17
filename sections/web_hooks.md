# Web Hooks

<!-- TOC -->

- [Attributes](#attributes)
- [GET /account/web_hooks](#get-accountweb_hooks)
- [GET /account/web_hooks/{id}](#get-accountweb_hooksid)
- [POST /account/web_hooks](#post-accountweb_hooks)
- [PUT /account/web_hooks/{id}](#put-accountweb_hooksid)
- [PUT /account/web_hooks/{id}/disable](#put-accountweb_hooksiddisable)
- [PUT /account/web_hooks/{id}/enable](#put-accountweb_hooksidenable)
- [DELETE /account/web_hooks/{id}](#delete-accountweb_hooksid)

<!-- /TOC -->

## Attributes

```json
{
  "id": 123,
  "target": "Activity",
  "event": "create",
  "hook": "https://example.org/do-stuff",
  "disabled": false,
  "disabled_at": null,
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /account/web_hooks

Retrieve all web hooks:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/web_hooks' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array with complete web hooks information (see Attributes).

## GET /account/web_hooks/{id}

Retrieve a single web hook:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/account/web_hook/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns a single web hook representation.

## POST /account/web_hooks

Create a new web hook:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/account/web_hooks' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "target": "Activity",
        "event": "create",
        "hook": "https://example.org/do-stuff"
      }'
```

Mandatory fields are marked with a star (\*):

- **target\*** – "Activity" (Activity/Company/Contact/Project/Invoice/Offer/Deal/Expense)
- **event\*** – "create" (create/update/delete)
- **hook\*** – "https://example.org/do-stuff"

## PUT /account/web_hooks/{id}

Update the web hook:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/account/web_hooks/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "hook": "https://example.org/v2"
      }'
```

Fields are analogous to the POST request.

## PUT /account/web_hooks/{id}/disable

Disable the web hook (if already disabled, it does nothing):

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/account/web_hooks/{id}/disable' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## PUT /account/web_hooks/{id}/enable

Enable the web hook (if already enabled, it does nothing):

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/account/web_hooks/{id}/enable' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## DELETE /account/web_hooks/{id}

Removes the web hook:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/account/web_hooks/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
