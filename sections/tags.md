---
layout: default
parent: Entities
---

# Tags / Labels

<!-- TOC -->

- [GET /taggings](#get-taggings)
- [PATCH /taggings](#patch-taggings)
- [PUT /taggings](#put-taggings)
- [DELETE /taggings](#delete-taggings)

<!-- /TOC -->

The API provides a single endpoint to manage the tags (aka labels) associated to different type of entities:

```
/api/v1/taggings/{entity}/{entity_id}
```

The parameter `{entity}` can be one of the following:
Company, Contact, Project, Deal, Purchase, Invoice, Offer

## GET /taggings

Retrieve the list of tags associated with the entity:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/taggings/Project/357'
```

Returns an array with tag names:

```
["cool", "on hold"]
```

## PATCH /taggings

Add tags to the entity:

```bash
curl -X PATCH \
  'https://{domain}.mocoapp.com/api/v1/taggings/Project/357' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": ["cool", "on hold"]
      }'
```

This adds the tags "cool" and "on hold" to the project with ID 357 and returns the list of all the tags associated
to the project. Existing tags are preserved, so if the project had the tag "climate", in the end it will have 3 tags:
"climate", "cool" and "on hold".
If a tag is already assigned to the entity, then it's silently ignored.
If a tag doesn't exist, then it's created automatically.

## PUT /taggings

Replace the tags associated to the entity:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/taggings/Project/357' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": ["cool", "on hold"]
      }'
```

Similar to the previous operation but in this case existing tags are removed if not included in the set of the assigned tags.
So, if the project had the tag "climate", it ends up having only 2 tags:
"cool" and "on hold".
Also in this case, if a tag is already assigned to the entity, then it's silently ignored and if a tag doesn't exist,
then it's created automatically.

This operation can be used to clean out the tags of an entity just passing an empty array as `tags`.

## DELETE /taggings

Selectively remove the tags associated to the entity:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/taggings/Project/357' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": ["cool"]
      }'
```

Other tags are preserved, so if the project had "cool" and "on hold", it ends up having just "on hold". If any mentioned tag
is not associated to the entity, it's silently ignored.
