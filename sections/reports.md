# Reports

German: "Berichte"

<!-- TOC -->

- [GET /report/users_absences](#get-reportusers_absences)

<!-- /TOC -->

## GET /report/users_absences

Retrieve a list of absences per user:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/report/users_absences' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

It's also possible to filter:

- **active** - true/false (include only absences for active users, defaults to false)
- **year** - 2021 (defaults to current year)

This returns an array with the following structure:

```json
[
  {
    "id": 123,
    "firstname": "Jane",
    "lastname": "Doe",
    "used_vacations": 10.5,
    "planned_vacations": 5.0,
    "rest_vacations": 9.5,
    "sickness": 4.0
  }
]
```
