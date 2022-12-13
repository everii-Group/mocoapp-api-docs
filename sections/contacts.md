---
layout: default
parent: Entities
---

# Contacts

German: "Kontakte / Ansprechpartner"

- TOC
{:toc}

## Attributes

Includes among the standard fields for contacts also:

- Tags
- Company (if this contact belongs to a company)

```json
{
  "id": 123,
  "gender": "M",
  "firstname": "Peter",
  "lastname": "Muster",
  "title": "Dr. med.",
  "job_position": "Account Manager",
  "mobile_phone": "+41 123 45 67",
  "work_fax": "",
  "work_phone": "+41 445 45 67",
  "work_email": "peter.muster@beispiel.ch",
  "work_address": "Beispiel AG\nPeter Muster\nBeispielstrasse 123",
  "home_email": "",
  "home_address": "",
  "birthday": "1959-05-22",
  "info": "",
  "avatar_url": "https//meinefirma.mocoapp.com/.../profil.jpg",
  "tags": ["Key Account", "Christmas Card"],
  "company": {
    "id": 123456,
    "type": "customer",
    "name": "Beispiel AG"
  },
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /contacts/people

Retrieve all contacts:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/contacts/people' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's also possible to filter:

- **ids** – e.g. `123,456` (IDS, comma-separated)
- **updated_after** - e.g. `2022-09-01T14:00:00Z` ISO8601 timestamp, only records that have been updated/created after
- **tags** "Influencer, Early Adopter" (comma separated list)
- **term** "mario, volkswagen" (full text search name, firstname, work_email, company)
- **phone** 79 826 (reverse lookup for work_phone or mobile_phone)

Returns an array with all contact information (see attributes), except `info`.

## GET /contacts/people/{id}

Retrieve a single contact:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/contacts/people/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Returns the representation for a single contact, including tags and the company.

## POST /contacts/people

Create a contact:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/contacts/people' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "firstname": "Peter",
        "lastname": "Muster",
        "birthday": "1959-05-22"
      }'
```

Mandatory fields are marked with a star (\*):

- **firstname\*** – "Peter"
- **lastname\*** – "Muster"
- **gender\*** – "F", "M" or "U"
- **company_id** – 123
- **user_id** - 456 (responsible for this contact), current user is default
- **title** – "Dr. med."
- **job_position** – "Account Manager"
- **mobile_phone** – "+49 177 123 45 67"
- **work_fax** – "+49 30 123 45 67"
- **work_phone** – "+49 30 123 45 67"
- **work_email** – "bestellung@lieferant.de"
- **work_address** – "Lieferant AG\nBeispielstrasse 123\n12345 Berlin"
- **home_email** – "privat@home.ch"
- **home_address** – "Peter Muster\nZu Hause"
- **birthday** – "1959-05-22"
- **info** – "Information for this company"
- **tags** – ["Christmas Card", "Project Lead"]

## PUT /contacts/people/{id}

Update a contact:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/contacts/people/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "job_position": "Head of Sales"
      }'
```

Fields are analogous to the POST request.

## DELETE /contacts/people/{id}

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/contacts/people/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```
