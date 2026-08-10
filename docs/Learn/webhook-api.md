---
title: Webhook API
excerpt: >-
  Programmatically manage your CloudContactAI webhooks using the Webhook Management API.
deprecated: false
hidden: false
metadata:
  title: CloudContactAI Webhook Management API
  description: How to programmatically list, create, update, and delete webhooks with the CloudContactAI API
  robots: index
---

> Manage your webhooks programmatically to dynamically add, update, and remove webhook subscriptions.

## Overview

The CloudContactAI Webhook Management API allows you to programmatically manage webhook subscriptions for your account. Instead of configuring webhooks manually through the dashboard, you can use these endpoints to dynamically register, update, list, and delete webhooks from your application.

**Base URL:** `https://core.cloudcontactai.com/api`

## Authentication

All requests require authentication. Include your API key in the request headers:

```
Authorization: Bearer YOUR_API_KEY
```

## Endpoints

### List Webhooks

Retrieve all registered webhooks for a client.

**Request:**

```
GET /v1/client/{clientId}/integration
```

**Example (cURL):**

```bash
curl -X GET https://core.cloudcontactai.com/api/v1/client/YOUR_CLIENT_ID/integration \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

**Example (Node.js with SDK):**

```javascript
const ccai = new CCAI({ apiKey: 'YOUR_API_KEY', clientId: 'YOUR_CLIENT_ID' });
const webhooks = await ccai.webhooks.list();
console.log(webhooks);
```

**Example (Node.js with fetch):**

```javascript
const clientId = 'YOUR_CLIENT_ID';

const response = await fetch(`https://core.cloudcontactai.com/api/v1/client/${clientId}/integration`, {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY',
    'Content-Type': 'application/json'
  }
});

const webhooks = await response.json();
console.log(webhooks);
```

**Example (Python):**

```python
import requests

client_id = 'YOUR_CLIENT_ID'

response = requests.get(
    f'https://core.cloudcontactai.com/api/v1/client/{client_id}/integration',
    headers={
        'Authorization': 'Bearer YOUR_API_KEY',
        'Content-Type': 'application/json'
    }
)

webhooks = response.json()
print(webhooks)
```

**Response:**

```json
[
  {
    "id": "12345",
    "url": "https://your-app.com/webhook",
    "method": "POST",
    "integrationType": "ALL"
  }
]
```

---

### Get Single Webhook

Retrieve a specific webhook by its ID.

**Request:**

```
GET /v1/client/{clientId}/integration/{webhookId}
```

**Example (cURL):**

```bash
curl -X GET https://core.cloudcontactai.com/api/v1/client/YOUR_CLIENT_ID/integration/12345 \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

**Example (Node.js with fetch):**

```javascript
const clientId = 'YOUR_CLIENT_ID';
const webhookId = '12345';

const response = await fetch(`https://core.cloudcontactai.com/api/v1/client/${clientId}/integration/${webhookId}`, {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY',
    'Content-Type': 'application/json'
  }
});

const webhook = await response.json();
console.log(webhook);
```

**Example (Python):**

```python
import requests

client_id = 'YOUR_CLIENT_ID'
webhook_id = '12345'

response = requests.get(
    f'https://core.cloudcontactai.com/api/v1/client/{client_id}/integration/{webhook_id}',
    headers={
        'Authorization': 'Bearer YOUR_API_KEY',
        'Content-Type': 'application/json'
    }
)

webhook = response.json()
print(webhook)
```

---

### Register Webhook

Create a new webhook subscription. The request body is an array, allowing you to register multiple webhooks in a single call.

**Request:**

```
POST /v1/client/{clientId}/integration
```

**Request Body (array):**

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `url` | string | Yes | The HTTPS endpoint URL where events will be sent |
| `method` | string | No | HTTP method for delivery (POST or PUT). Defaults to POST |
| `integrationType` | string | No | Type of events to receive. Defaults to ALL |
| `secretKey` | string | No | Secret key for signature verification. Auto-generated if not provided |

**Example (cURL):**

```bash
curl -X POST https://core.cloudcontactai.com/api/v1/client/YOUR_CLIENT_ID/integration \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '[{
    "url": "https://your-app.com/webhook",
    "method": "POST",
    "integrationType": "ALL"
  }]'
```

**Example (Node.js with SDK):**

```javascript
const ccai = new CCAI({ apiKey: 'YOUR_API_KEY', clientId: 'YOUR_CLIENT_ID' });

const webhook = await ccai.webhooks.register({
  url: 'https://your-app.com/webhook',
  integrationType: 'ALL'
});

console.log(`Webhook ID: ${webhook.id}`);
console.log(`Secret Key: ${webhook.secretKey}`);
```

**Example (Node.js with fetch):**

```javascript
const clientId = 'YOUR_CLIENT_ID';

const response = await fetch(`https://core.cloudcontactai.com/api/v1/client/${clientId}/integration`, {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify([{
    url: 'https://your-app.com/webhook',
    method: 'POST',
    integrationType: 'ALL'
  }])
});

const result = await response.json();
console.log(result);
```

**Example (Python):**

```python
import requests

client_id = 'YOUR_CLIENT_ID'

response = requests.post(
    f'https://core.cloudcontactai.com/api/v1/client/{client_id}/integration',
    headers={
        'Authorization': 'Bearer YOUR_API_KEY',
        'Content-Type': 'application/json'
    },
    json=[{
        'url': 'https://your-app.com/webhook',
        'method': 'POST',
        'integrationType': 'ALL'
    }]
)

result = response.json()
print(result)
```

**Response:**

```json
[
  {
    "id": "12345",
    "url": "https://your-app.com/webhook",
    "method": "POST",
    "integrationType": "ALL",
    "secretKey": "generated-secret-key-here"
  }
]
```

---

### Update Webhook

Update an existing webhook. Uses the same `POST` endpoint as registration, but includes the webhook `id` in the payload to indicate an update.

**Request:**

```
POST /v1/client/{clientId}/integration
```

**Request Body (array):**

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | integer | Yes | The ID of the webhook to update |
| `url` | string | Yes | Updated HTTPS endpoint URL |
| `method` | string | No | HTTP method (POST or PUT). Defaults to POST |
| `integrationType` | string | No | Type of events to receive. Defaults to ALL |
| `secretKey` | string | No | Updated secret key (only if you want to change it) |

**Example (cURL):**

```bash
curl -X POST https://core.cloudcontactai.com/api/v1/client/YOUR_CLIENT_ID/integration \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '[{
    "id": 12345,
    "url": "https://your-app.com/webhook-v2",
    "method": "POST",
    "integrationType": "ALL"
  }]'
```

**Example (Node.js with SDK):**

```javascript
const ccai = new CCAI({ apiKey: 'YOUR_API_KEY', clientId: 'YOUR_CLIENT_ID' });

const updated = await ccai.webhooks.update('12345', {
  url: 'https://your-app.com/webhook-v2',
  integrationType: 'ALL'
});

console.log(updated);
```

**Example (Node.js with fetch):**

```javascript
const clientId = 'YOUR_CLIENT_ID';

const response = await fetch(`https://core.cloudcontactai.com/api/v1/client/${clientId}/integration`, {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify([{
    id: 12345,
    url: 'https://your-app.com/webhook-v2',
    method: 'POST',
    integrationType: 'ALL'
  }])
});

const result = await response.json();
console.log(result);
```

**Example (Python):**

```python
import requests

client_id = 'YOUR_CLIENT_ID'

response = requests.post(
    f'https://core.cloudcontactai.com/api/v1/client/{client_id}/integration',
    headers={
        'Authorization': 'Bearer YOUR_API_KEY',
        'Content-Type': 'application/json'
    },
    json=[{
        'id': 12345,
        'url': 'https://your-app.com/webhook-v2',
        'method': 'POST',
        'integrationType': 'ALL'
    }]
)

result = response.json()
print(result)
```

---

### Delete Webhook

Remove a webhook subscription by its ID.

**Request:**

```
DELETE /v1/client/{clientId}/integration/{webhookId}
```

**Example (cURL):**

```bash
curl -X DELETE https://core.cloudcontactai.com/api/v1/client/YOUR_CLIENT_ID/integration/12345 \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

**Example (Node.js with SDK):**

```javascript
const ccai = new CCAI({ apiKey: 'YOUR_API_KEY', clientId: 'YOUR_CLIENT_ID' });

const result = await ccai.webhooks.delete('12345');
console.log(result); // { success: true, message: '...' }
```

**Example (Node.js with fetch):**

```javascript
const clientId = 'YOUR_CLIENT_ID';
const webhookId = '12345';

const response = await fetch(`https://core.cloudcontactai.com/api/v1/client/${clientId}/integration/${webhookId}`, {
  method: 'DELETE',
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY',
    'Content-Type': 'application/json'
  }
});

if (response.ok) {
  console.log('Webhook deleted successfully');
}
```

**Example (Python):**

```python
import requests

client_id = 'YOUR_CLIENT_ID'
webhook_id = '12345'

response = requests.delete(
    f'https://core.cloudcontactai.com/api/v1/client/{client_id}/integration/{webhook_id}',
    headers={
        'Authorization': 'Bearer YOUR_API_KEY',
        'Content-Type': 'application/json'
    }
)

if response.status_code == 200:
    print('Webhook deleted successfully')
```

---

## Webhook Signature Verification

When you register a webhook, CloudContactAI returns a `secretKey` (or you can provide your own). This key is used to sign each webhook delivery so you can verify it came from CloudContactAI.

The signature is sent in the `X-CCAI-Signature` header and is computed as:

```
HMAC-SHA256(secretKey, "{clientId}:{eventHash}")
```

The result is Base64-encoded.

**Verification example (Node.js with SDK):**

```javascript
const isValid = ccai.webhooks.verifySignature(
  req.headers['x-ccai-signature'],  // Signature from header
  clientId,                          // Your client ID
  payload.eventHash,                 // eventHash from the payload
  'your-secret-key'                  // Secret key from registration
);

if (!isValid) {
  return res.status(401).send('Invalid signature');
}
```

**Verification example (Python):**

```python
import hmac
import hashlib
import base64

def verify_webhook_signature(signature, client_id, event_hash, secret_key):
    data = f"{client_id}:{event_hash}"
    computed = base64.b64encode(
        hmac.new(secret_key.encode(), data.encode(), hashlib.sha256).digest()
    ).decode()
    return hmac.compare_digest(signature, computed)
```

---

## Integration Types

| Value | Description |
|-------|-------------|
| `ALL` | Receive all event types |

---

## Use Cases

**Dynamic environment setup:** Automatically register webhooks when deploying a new environment, and clean them up when tearing it down.

**Multi-tenant applications:** Programmatically create separate webhook subscriptions for each tenant in your application.

**Webhook rotation:** Update the destination URL when migrating services or rotating endpoints for security purposes.

**Automated testing:** Register a temporary webhook endpoint during integration tests and delete it after the test run completes.
