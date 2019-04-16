# Schedules

German: "Planung"

## Attributes

The planning entry representation contains among the standard fields also:

- assignment (project assignment or absence)
- assigned user (staff)

```json
{
  "id": 123,
  "date": "2017-06-14",
  "comment": "Half day off",
  "am": true,
  "pm": true,
  "assignment": {
    "id": 789,
    "name": "Holiday",
    "customer_name": "hundertzehn GmbH",
    "color": "#BBB",
    "type": "Absence"
  },
  "user": {
    "id": 567,
    "firstname": "Sabine",
    "lastname": "Schäuble"
  },
  "created_at": "2018-10-17 09:33:46 UTC",
  "updated_at": "2018-10-17 09:33:46 UTC"
}
```

## GET /schedules

Retrieve all planning entries (paged):

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/schedules?from=2018-10-01&to=2018-10-31' \
  -H 'Authorization: Token token={api-key}'
```

This returns an array with complete schedule information (see Attributes).

Additionally, the following parameters can be supplied:

- **from** – "2017-05-01"
- **to** – "2017-05-31"
- **user_id** – 123
- **project_id** – 345 or **absence_code** – 1, 2, 3, 4 (absence, public holiday, sick day, holiday)

## GET /schedules/{id}

Retrieve a single planning entry:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/schedules/{id}' \
  -H 'Authorization: Token token={api-key}'
```

## POST /schedules

Create a planning entry:

The entry is always created with the user that's executing the request (authorization token) if no `user_id` is supplied.

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/schedules' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "date": "2018-10-01",
        "project_id": 123456,
      }'
```

Mandatory fields are marked with a star (\*):

- **date\*** – "2017-06-11"
- **project_id\*** – 123456 or **absence_code\*** – 1, 2, 3, 4 (absence, public holiday, sick day, holiday)
- **user_id** – 234567 (user ID for active staff)
- **am** – true, false (morning yes/no)
- **pm** – true, false (afternoon yes/no)
- **comment** – "A comment..."
- **overwrite** – true, false (override existing entry)

## PUT /schedules/{id}

Update a planning entry:

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/schedules/{id}' \
  -H 'Authorization: Token token={api-key}' \
  -H 'Content-Type: application/json' \
  -d '{
        "comment": "A comment",
      }'
```

Fields are analogous to the POST request.

## DELETE /schedules/{id}

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/schedules/{id}' \
  -H 'Authorization: Token token={api-key}'
```
