# Custom Fields

MOCO supports adding custom fields to many of its resources. These custom fields are readable and writable via the `custom_properties` field.

**NOTE**: The size of the custom_properties field is limitted to 12 kB.

```json
"custom_properties": {
    "UID": "123-UID-456",
    "Line of business": "Automotive"
}
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

**NOTE**: The provided custom properties are merged with the existing custom properties of the entity. That is, only the provided custom properties are updated and the other custom properties of the entity are left unchanged.