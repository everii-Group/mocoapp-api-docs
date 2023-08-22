---
layout: default
parent: Entities
---

# Profile

German: "Profil"

- TOC
{:toc}

## GET /profile

Get the current user's profile. If [impersonation](../index#impersonation) is used, it's the impersonated user.

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/profile' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

The profile returned:

```json
{
  "id": 237852983,
  "email": "janine.kuesters@meinefirma.de",
  "full_name": "Janine Küsters",
  "first_name": "Janine",
  "last_name": "Küsters",
  "active": true,
  "external": false,
  "avatar_url": "https://data.mocoapp.com/objects/6bf3db0a-895a-46a1-8006-6280af04b9c0.jpg",
  "unit": {
    "id": 436796,
    "name": "Design"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2022-08-02T14:21:56Z"
}
```