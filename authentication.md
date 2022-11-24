# Authentication

You need an API key for authentication. Each user can find their user-specific key on mocoapp.com on their profile in the "Integrations" tab. This key is provided as an Authorization header.

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/projects.json' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

This key can also be requested via API:

```bash
curl -X POST \
  https://{domain}.mocoapp.com/api/v1/session \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "email": "max@muster.de",
    "password": "secret"
  }'
```

It's also possible to verify if the API key is still valid:

```bash
curl https://{domain}.mocoapp.com/api/v1/session \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json'
```

If the key is valid, the response code id `200 ok` and the body is:

```json
{
  "id": 123,
  "uuid": "aec324a2-4832-11eb-b378-0242ac130002"
}
```

otherwise the response code is `401 unauthorized`.

## Postman example

There are a few tools to try out the MOCO API. All the examples in this documentation use `curl` to demonstrate the API endpoint.
A popular graphical UI for REST is [Postman](https://www.postman.com/). Here's an example request for the projects list including the authentication:

![Postman example request](moco-api-postman.png "Postman example request")