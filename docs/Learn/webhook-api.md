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

**Base URL:** `https://core.cloudcontactai.com`

## Authentication

All requests require authentication. Include your API key in the request headers:

```
Authorization: Bearer YOUR_API_KEY
```

## Endpoints

### List Webhooks

Retrieve all registered webhooks for your account.

**Request:**

```
GET /api/webhooks
```

**Example (cURL):**

```bash
curl -X GET https://core.cloudcontactai.com/api/webhooks \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

**Example (Node.js):**

```javascript
const response = await fetch('https://core.cloudcontactai.com/api/webhooks', {
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

response = requests.get(
    'https://core.cloudcontactai.com/api/webhooks',
    headers={
        'Authorization': 'Bearer YOUR_API_KEY',
        'Content-Type': 'application/json'
    }
)

webhooks = response.json()
print(webhooks)
```

---

### Register Webhook

Create a new webhook subscription.

**Request:**

```
POST /api/webhooks
```

**Request Body:**

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `url` | string | Yes | The HTTPS endpoint URL where events will be sent |
| `events` | array | Yes | List of event types to subscribe to |
| `method` | string | No | HTTP method for delivery (POST or PUT). Defaults to POST |

**Example (cURL):**

```bash
curl -X POST https://core.cloudcontactai.com/api/webhooks \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://your-app.com/webhook",
    "events": ["message.sent", "message.incoming", "contact.unsubscribed"],
    "method": "POST"
  }'
```

**Example (Node.js):**

```javascript
const response = await fetch('https://core.cloudcontactai.com/api/webhooks', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    url: 'https://your-app.com/webhook',
    events: ['message.sent', 'message.incoming', 'contact.unsubscribed'],
    method: 'POST'
  })
});

const webhook = await response.json();
console.log(webhook);
```

**Example (Python):**

```python
import requests

response = requests.post(
    'https://core.cloudcontactai.com/api/webhooks',
    headers={
        'Authorization': 'Bearer YOUR_API_KEY',
        'Content-Type': 'application/json'
    },
    json={
        'url': 'https://your-app.com/webhook',
        'events': ['message.sent', 'message.incoming', 'contact.unsubscribed'],
        'method': 'POST'
    }
)

webhook = response.json()
print(webhook)
```

**Available Event Types:**

- `message.sent`
- `message.incoming`
- `message.excluded`
- `message.error.carrier`
- `message.error.cloudcontact`
- `contact.unsubscribed`

For details on each event type, see the [Webhook Event Types](https://developer.cloudcontactai.com/docs/webhooks-types) page.

---

### Update Webhook

Update an existing webhook subscription by its ID.

**Request:**

```
PUT /api/webhooks/{id}
```

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | string | The unique identifier of the webhook to update |

**Request Body:**

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `url` | string | No | Updated HTTPS endpoint URL |
| `events` | array | No | Updated list of event types |
| `method` | string | No | Updated HTTP method (POST or PUT) |

**Example (cURL):**

```bash
curl -X PUT https://core.cloudcontactai.com/api/webhooks/12345 \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://your-app.com/webhook-v2",
    "events": ["message.sent", "message.incoming", "message.error.carrier", "contact.unsubscribed"]
  }'
```

**Example (Node.js):**

```javascript
const webhookId = '12345';

const response = await fetch(`https://core.cloudcontactai.com/api/webhooks/${webhookId}`, {
  method: 'PUT',
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    url: 'https://your-app.com/webhook-v2',
    events: ['message.sent', 'message.incoming', 'message.error.carrier', 'contact.unsubscribed']
  })
});

const updatedWebhook = await response.json();
console.log(updatedWebhook);
```

**Example (Python):**

```python
import requests

webhook_id = '12345'

response = requests.put(
    f'https://core.cloudcontactai.com/api/webhooks/{webhook_id}',
    headers={
        'Authorization': 'Bearer YOUR_API_KEY',
        'Content-Type': 'application/json'
    },
    json={
        'url': 'https://your-app.com/webhook-v2',
        'events': ['message.sent', 'message.incoming', 'message.error.carrier', 'contact.unsubscribed']
    }
)

updated_webhook = response.json()
print(updated_webhook)
```

---

### Delete Webhook

Remove a webhook subscription by its ID.

**Request:**

```
DELETE /api/webhooks/{id}
```

**Path Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | string | The unique identifier of the webhook to delete |

**Example (cURL):**

```bash
curl -X DELETE https://core.cloudcontactai.com/api/webhooks/12345 \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

**Example (Node.js):**

```javascript
const webhookId = '12345';

const response = await fetch(`https://core.cloudcontactai.com/api/webhooks/${webhookId}`, {
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

webhook_id = '12345'

response = requests.delete(
    f'https://core.cloudcontactai.com/api/webhooks/{webhook_id}',
    headers={
        'Authorization': 'Bearer YOUR_API_KEY',
        'Content-Type': 'application/json'
    }
)

if response.status_code == 200:
    print('Webhook deleted successfully')
```

---

## Use Cases

**Dynamic environment setup:** Automatically register webhooks when deploying a new environment, and clean them up when tearing it down.

**Multi-tenant applications:** Programmatically create separate webhook subscriptions for each tenant in your application.

**Event filtering:** Update your webhook subscription to add or remove event types as your application's needs evolve.

**Webhook rotation:** Update the destination URL when migrating services or rotating endpoints for security purposes.
