# Custom Fields

MOCO supports adding custom fields to many of its resources. These custom fields are readable and writable via the `custom_properties` field.

```json
"custom_properties": {
    "UID": "123-UID-456",
    "Line of business": "Automotive"
},
```

Parameters are sent with their name as key:

```bash
curl -X POST \
  https://{domain}.mocoapp.com/api/v1/customers \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Beispiel AG",
    "currency": "CHF",
    "custom_properties": {
      "Line of business": "Automotive"
    }
  }'
```

All values are encoded as strings, expect for Multiple Choice, which is encoded as an array.

```bash
curl -X POST \
  https://{domain}.mocoapp.com/api/v1/customers \
  -H 'Authorization: Token token=YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
        "custom_properties": {
          "Line of business": ["Automotive", "Banking"]
        }
      }'
```

- Single-line input – "Automotive"
- Mehrzeilige Eingabe – "A multiline input..."
- Link – "https://www..."
- Date – "2021-12-31"
- Yes/No – "0", "1" (0 = No, 1 = Yes)
- Single choice – "Value"
- Multiple choice – ["Value 1", "Value 2"]

⚡ **WARNING** ⚡: If you use custom fields, all of them have to be provided. If not, any that are not transmitted will be removed.