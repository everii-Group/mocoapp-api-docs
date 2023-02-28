---
layout: default
parent: Entities
---

# Reports

German: "Berichte"

- TOC
{:toc}

## GET /report/absences

Retrieve a list of absences per user:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/report/absences' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's also possible to filter:

- **active** - true/false (include only absences for active users, defaults to false)
- **year** - 2021 (defaults to current year)

This returns an array with the following structure:

```json
[
  {
    "user": {
      "id": 123,
      "firstname": "Jane",
      "lastname": "Doe"
    },
    "total_vacation_days": 25.0,
    "used_vacation_days": 10.5,
    "planned_vacation_days": 5.0,
    "sickdays": 4.0
  }
]
```
