---
layout: default
title: Letter Papers
parent: Entities
---

# Letter Papers

German: "Briefpapier"

- TOC
{:toc}

## Attributes

Letter paper attributes:

- **id** – Unique identifier
- **name** – Name of the letter paper
- **active** – Whether the letter paper is active (`true` / `false`)
- **template** – Template identifier (e.g., "invoice", "offer", "timesheet`) or `null`
- **file** – URL to the letter paper PDF file or `null`
- **created_at** – Creation timestamp (UTC, ISO8601)
- **updated_at** – Last update timestamp (UTC, ISO8601)

```json
{
  "id": 123,
  "name": "Standard Letter Paper",
  "active": true,
  "template": "invoice",
  "file": "https://data.mocoapp.com/objects/.../letter_paper.pdf",
  "created_at": "2024-01-15T10:30:00Z",
  "updated_at": "2024-03-20T14:45:00Z"
}
```

## GET /letter_papers

Retrieve all letter papers:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/letter_papers' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

returns an array of letter papers.

The following parameters can be supplied:

- **page** – Page number (default: 1)
- **per_page** – Number of items per page (default: 100, max: 1000)
- **ids** – Comma-separated list of IDs to filter by
- **updated_after** – ISO8601 timestamp to filter for items updated after a specific time

Example with pagination:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/letter_papers?page=1&per_page=100' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

The response includes pagination headers:

- **X-Page** – Current page number
- **X-Per-Page** – Number of items per page
- **X-Total** – Total number of items
- **Link** – Link to the next page (if available)
