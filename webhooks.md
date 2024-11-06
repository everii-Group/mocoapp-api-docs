# WebHooks

Check the [MOCO docs](https://www.mocoapp.com/integrationen/35-moco-webhooks) on how to set them up via the web UI. It's also possible to manage them via [API](sections/web_hooks).

Using WebHooks, integrating any system in real time becomes possible. Events in MOCO can be assigned subscriptions.
Whenever an event triggers, MOCO sends an HTTPS `POST` payload to the WebHook's configured URL with an HMAC SHA265 signature.
This way, MOCOs integrity as a legitimate sender of this information can be verified. Additional headers provide context
for the sent payload.

- **X-Moco-Target** – Activity, Customer, Project, ...
- **X-Moco-Event** – create, update, delete, archive, ...
- **X-Moco-Timestamp** – Timestamp for this event
- **X-Moco-Signature** – The signature fo this request, see comment below for details
- **X-Moco-User-Id** – The user ID that triggered this hook
- **X-Moco-Account-Url** – The subdomain for the account
- The receiver has to process the request within 10 seconds

The following example shows a WebHook triggered by an activity creation.

```
X-Moco-Target: Activity
X-Moco-Event: create
X-Moco-Timestamp: 1527170410463
X-Moco-Signature: f457bffc50e9b63f455ab107c55f2f61956550aa5525c2cfe07f574014bd8a9e
X-Moco-User-Id: 933613686
```

- To debug and try out web hooks, we recommend [webhook.site](https://webhook.site) or [requestbin.com](https://requestbin.com/) – this services provides you with temporary
  HTTPS URLs that let you inspect any incoming WebHook data.
- WebHooks are only provided to customers after they subscribe to MOCO.
- WebHooks are not guaranteed to be delivered in order. Pay attention to the provided time stamp if this is important
  for your use case.
- The signature uses HMAC with SHA256 to sign the whole payload. The key for the signature is the 32 characters
  hexadecimal string displayed in the web hook overview.

## Calculating the signature

OpenSSL CLI:

```bash
$ echo -n '{"id":111,"description":"a description"}' | openssl sha256 -hmac "1d608b9d72219b90ff2393a1d3ee0ac0"
SHA2-256(stdin)= bf027a86207ef1ca1cb76f5a536b41a14287ab1a0fd5b33bfe86924bc2f48fd1
```

Ruby:

```ruby
payload = '{"id":111,"description":"a description"}' 
signature_key = "1d608b9d72219b90ff2393a1d3ee0ac0"
payload_signature = OpenSSL::HMAC.hexdigest("SHA256", signature_key, payload)
# => "bf027a86207ef1ca1cb76f5a536b41a14287ab1a0fd5b33bfe86924bc2f48fd1"
```

NodeJS:

```javascript
const crypto = require("crypto");
const hmac = crypto.createHmac("sha256", "1d608b9d72219b90ff2393a1d3ee0ac0");
const data = hmac.update('{"id":111,"description":"a description"}');
const digest = data.digest("hex");
console.log("digest = " + digest);
```

## Notes

- We expect a successful response code for the Webhook request (i.e. any 2XX code), otherwise it's considered a failure
  and it's retried.
- After a few seconds we cancel your request (timeout), so avoid any heavy/synchronous work and consider pushing to a queue for further processing
- After 500 consecutive failures a Webhook is automatically disabled.
