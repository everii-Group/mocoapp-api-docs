---
layout: default
title: Moco API Documentation
nav_exclude: true
---

# MOCO API Documentation

This is the official API documentation for [mocoapp.com](https://www.mocoapp.com).

* TOC
{:toc}

## General

- Request payloads to MOCO must be sent as valid JSON with a mandatory `Content-Type: application/json`-header. Responses are also sent as JSON.
- All requests have to be [authenticated](authentication) with a key
- Example responses showcase the happy case, i.e. usually the `200 OK` response
- Collections are usually [paginated](#pagination)
- Zapier triggers are **not** triggered for API requests
- Timestamps `created_at` and `updated_at` are sent for all entities in UTC, as ISO8601 format.
- For synchronization almost all resources can be filtered by `updated_after` passing a time in UTC, as ISO8601 format.
- MOCO does not support any client-libraries at the moment. However, there are currently the following unofficial clients available, which you can use at your risk: [Python Client](https://github.com/sommalia/moco-wrapper)

## Entities

All the entities exposed via the API can be found in their [respective sections](entities.md)

## Client Implementations / API Wrappers

Here's a list of API client implementations, not maintained by us. Feel free to open up a PR to point to your implementation so others can re-use it.

| Language |                Repository                        |
| -------- | :----------------------------------------------: |
| Python   | https://github.com/sommalia/moco-wrapper         |
| PHP      | https://github.com/mbs-hub/moco-php              |
| Ruby     | https://github.com/starsong-consulting/moco-ruby |

## Impersonation

By default all requests are scoped to the authenticated user. Some resources cannot be provided with a `user_id` or similar, like `Activities` and `User Presences`. This reflects the behaviour in the UI, since every user can only create their own activities or presences. But you can login as another user provided that the authenticated user has permission to _Staff_. To achieve the same behaviour in the API, one can set the following x-header:

`X-IMPERSONATE-USER-ID=123` (user id to act in behalf of)

## Rate Limiting

You can expect to be able to send 120 requests per 2 minutes (~ 1 request per second). For the unlimited plan, its 1200 requests per 2 minutes (~ 10 per second). If you exceed this limit, the server responds with `429 Too Many Requests`.

## Pagination

Responses are paginated with a common default of 100 entries per page. In the HTTP response header, the current page, the entries per page and the number of total entries is reported. There is also a link header to links to the consecutive page.

- **X-Page** – 3
- **X-Per-Page** – 100
- **X-Total** – 415
- **Link** – `<https://{domain}.mocoapp.com/api/v1/projects.json?page=4>; rel="next"`

If there is not Link header with `rel="next"`, the current page is the last page.

## Errors and HTTP status codes

The MOCO-API is mostly conformant with the [general HTTP status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

Here are the most comment errors you will see:

- **401 Unauthorized** - Check the error message in the response body
- **403 Forbidden** - Check your [Authentication](#authentication) or your MOCO user permission
- **404 Not Found** - Check that resource exists (maybe it was deleted in the meantime)
- **422 Unprocessable Entity** - Check the provided error message in the response body
- **429 Too Many Requests** - Check [Rate Limiting](#rate-limiting)

## Sorting

Sorting is controlled by the `sort_by` query parameter. Its value is the field name that should be sorted, followed by an optional sorting order (`asc` or `desc`, default is `asc`).

Example:

- `https://{domain}.mocoapp.com/api/v1/offers?sort_by=title desc`
  


