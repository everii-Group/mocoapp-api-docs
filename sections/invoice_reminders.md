# Invoice Reminders BETA

German: "Mahnung / Zahlungserinnerung"

## Attributes

The invoice reminder representation contains among standard fields also shortened invoice information.

```json
{
  "id": 1,
  "title": "Zahlungserinnerung",
  "salutation": "Bei der Bearbeitung unserer Buchhaltung ist uns aufgefallen, dass wir für folgende Rechnung noch keinen Zahlungseingang verbuchen konnten.",
  "footer": "Sicherlich handelt es sich hierbei um ein Versehen. Wir bitten Sie höflich, uns den Betrag in den nächsten Tagen zu überweisen. Sollte sich Ihre Zahlung mit diesem Schreiben gekreuzt haben, betrachten Sie diese Erinnerung als gegenstandslos.",
  "fee": 0.0,
  "date": "2019-10-16",
  "due_date": "2019-10-30",
  "invoice": {
    "id": 1489,
    "identifier": "1409-019",
    "title": "Rechnung - Android Prototype"
  },
  "created_at": "2019-10-30T07:20:40Z",
  "updated_at": "2020-03-19T09:13:44Z"
}
```

## GET /invoice_reminders

Retrieve all invoice reminders:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoice_reminders' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

Additionally, these parameters can be used to filter the results set:

- **invoice_id** – 123
- **date_from** – "2018-01-01"
- **date_to** – "2018-01-31"

## GET /invoice_reminders/{id}

Retrieve a single invoice reminder:

```bash
curl -X GET \
  'https://{domain}.mocoapp.com/api/v1/invoice_reminders/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /invoice_reminders

Create an invoice reminder:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/invoice_reminders' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "invoice_id": 546046,
        "title": "Mahnung",
        "salutation": "Hallo",
        "date": "2020-08-04",
        "due_date": "2020-09-12"
      }'
```

Mandatory fields are marked with a star (\*):

- **invoice_id\*** – 546046
- **title\*** – "Mahnung",
- **salutation** – "Hallo"
- **footer** – "Bye"
- **fee** – 50
- **date** – "2020-08-04"
- **due_date** – "2020-09-12"

## DELETE /invoice_reminders/{id}

Delete an invoice reminder:

```bash
curl -X DELETE \
  'https://{domain}.mocoapp.com/api/v1/invoices_reminders/{id}' \
  -H 'Authorization: Token token=YOUR_API_KEY'
```

## POST /invoice_reminders/{id}/send_email

Send the reminder by email:

```bash
curl -X POST \
  'https://{domain}.mocoapp.com/api/v1/invoice_reminders/{id}/send_email' \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "emails_to": "somebody@example.com",
        "subject": "reminder",
        "text": "pending invoice"
      }'
```

Mandatory fields are marked with a star (\*):

- **emails_to\*** – "somebody@example.com;info@example.com" (list of addresses separated by _;_)
- **subject\*** – "reminder",
- **text\*** – "pending invoice"
- **emails_cc** – "somebodyelse@example.com" (list of addresses separated by _;_)
- **emails_bcc** – "somebody@partner.example.com" (list of addresses separated by _;_)
- **letter_paper_id** – 131
