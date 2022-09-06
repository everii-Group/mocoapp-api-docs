# Activities

German: "Zeiteinträge"

<!-- TOC -->

- [Attributes](#attributes)
- [GET /activities](#get-activities)
- [GET /activities/{id}](#get-activitiesid)
- [POST /activities](#post-activities)
- [PUT /activities/{id}](#put-activitiesid)
- [PATCH /activities/{id}/start_timer](#patch-activitiesidstart_timer)
- [PATCH /activities/{id}/stop_timer](#patch-activitiesidstop_timer)
- [DELETE /activities/{id}](#delete-activitiesid)
- [POST /activities/disregard](#post-activitiesdisregard)

<!-- /TOC -->

## Attributes

Activities contain among the standard fields also:

- Project
- Customer
- Task (on the project)
- User (creator)

Attributes `remote_service`, `remote_id` und `remote_url` are set by the MOCO Browser extension and represent a ticket in an external system (Trello, Jira, etc.) that this activity's time was spent on.

```json
{
  "id": 982237015,
  "date": "2018-07-03",
  "hours": 1.25,
  "seconds": 4500,
  "description": "Analysis context and dependencies",
  "billed": false,
  "billable": false,
  "tag": "",
  "remote_service": "trello",
  "remote_id": "9qzOS8AA",
  "remote_url": "https://trello.com/c/9qzOS8AA/123-analyse",
  "project": {
    "id": 944587499,
    "name": "Website Relaunch",
    "billable": false
  },
  "task": {
    "id": 658636,
    "name": "Concept",
    "billable": false
  },
  "customer": {
    "id": 760253684,
    "name": "Example Inc."
  },
  "user": {
    "id": 933590696,
    "firstname": "John",
    "lastname": "Doe"
  },
  "hourly_rate": 150,
  "timer_started_at": null,
  "created_at": "2018-10-17T09:33:46Z",
  "updated_at": "2018-10-17T09:33:46Z"
}
```

## GET /activities

Retrieve all activities:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/activities?from=2018-06-01&to=2018-06-30&project_id=4242' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This returns an array of all activities.

The following parameters can be supplied:

- **from** – "2018-06-01"
- **to** – "2018-06-30"
- **user_id** – 123
- **project_id** – 345
- **task_id** – 789
- **company_id** – 234567
- **term** – "search terms" (search in tag, description and remote_id)

## GET /activities/{id}

Retrieve a single activity:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/activities/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /activities

Create an activity:

Every activity is created for the user that the API key belongs to.

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/activities' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "date": "2017-06-11",
        "description": "Analysis context and dependencies",
        "project_id": 123456,
        "task_id": 234567,
        "hours": 1.0
      }'
```

Mandatory fields are marked with a star (\*):

- **date\*** – "2017-06-11"
- **project_id\*** – 123456
- **task_id\*** – 234567
- **hours\*** – 1.0 💡 passing 0 will start a timer if date is today
- **seconds** – 3600 💡 to avoid rounding issues, instead of hours you can also pass seconds
- **description** – "Analysis context and dependencies"
- **billable** – true/false (default: `true` or dependent on project configuration)
- **tag** – "RMT-123" (any tag as a string)
- **remote_service** – jira (Allowed values are: "trello", "jira", "asana", "basecamp", "wunderlist", "basecamp2", "basecamp3", "toggl", "mite", "github", "youtrack")
- **remote_id** – PRJ-2342
- **remote_url** – https://jira.meinefirma.de/browse/PRJ-2342

## PUT /activities/{id}

Update an activity.

```bash
curl -X PUT \
  'https://{domain}.mocoapp.com/api/v1/activities/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "hours": 2.0
      }'
```

All fields are analogous to the POST request.

## PATCH /activities/{id}/start_timer

Start or continue a timer on an activity.

```bash
curl -X PATCH \
  'https://{domain}.mocoapp.com/api/v1/activities/{id}/start_timer' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
```

⚠️ The timer is only available for activities on the current day. If timer cannot be started a 422 will be returned.

## PATCH /activities/{id}/stop_timer

Stop a timer running on an activity.

```bash
curl -X PATCH \
  'https://{domain}.mocoapp.com/api/v1/activities/{id}/stop_timer' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
```

## DELETE /activities/{id}

Delete an activity.

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/activities/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

⚠️ Deleting an activity is only possible if this activity has not yet been billed or locked.

## POST /activities/disregard

Mark activities as "already billed".

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/activities/disregard' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "activity_ids": [47268, 47269],
        "reason": "Courtesy service as agreed",
        "company_id": 123456
      }'
```

Mandatory fields are marked with a star (\*):

- **reason\*** – "Courtesy service as agreed"
- **activity_ids\*** – [123, 234, 345]
- **company_id\*** – 123456 (customer ID these activities belong to)
- **project_id** – 234567 (project ID these activities belong to)
