---
title: CloudContactAI Contact API - Do Not Text Integration Guide
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

## API Reference

### Set Do-Not-Text Status

* **Endpoint:** `PUT https://core.cloudcontactai.com/api/account/do-not-text`
* **Content-Type:** `application/json`
* **Authorization:** `Bearer <YOUR_API_KEY>`

### Request Body

| Field       | Type    | Required | Description                               |
| ----------- | ------- | -------- | ----------------------------------------- |
| `clientId`  | string  | Yes      | Your CloudContactAI client ID             |
| `contactId` | string  | No*      | The contact's unique ID                   |
| `phone`     | string  | No*      | The contact's phone number (E.164 format) |
| `doNotText` | boolean | Yes      | `true` to opt out, `false` to opt back in |

> * You must provide either `contactId` or `phone` to identify the contact.

### Response Body

| Field       | Type    | Description                    |
| ----------- | ------- | ------------------------------ |
| `contactId` | string  | The contact's unique ID        |
| `phone`     | string  | The contact's phone number     |
| `doNotText` | boolean | The updated do-not-text status |

***

## JavaScript Examples

### 1. Set Do-Not-Text by Contact ID

```javascript
const response = await fetch("https://core.cloudcontactai.com/api/account/do-not-text", {
  method: "PUT",
  headers: {
    "Authorization": "Bearer <YOUR_API_KEY>",
    "Content-Type": "application/json",
    "Accept": "*/*"
  },
  body: JSON.stringify({
    clientId: "<YOUR_CLIENT_ID>",
    contactId: "your-contact-id",
    doNotText: true
  })
});

const data = await response.json();
console.log(`Contact ${data.contactId} do not text set to ${data.doNotText}`);
```

### 2. Set Do-Not-Text by Phone Number

```javascript
const response = await fetch("https://core.cloudcontactai.com/api/account/do-not-text", {
  method: "PUT",
  headers: {
    "Authorization": "Bearer <YOUR_API_KEY>",
    "Content-Type": "application/json",
    "Accept": "*/*"
  },
  body: JSON.stringify({
    clientId: "<YOUR_CLIENT_ID>",
    phone: "+15551234567",
    doNotText: true
  })
});

const data = await response.json();
console.log(`Contact ${data.contactId} (${data.phone}) do not text set to ${data.doNotText}`);
```

### 3. Remove Do-Not-Text Status

```javascript
const response = await fetch("https://core.cloudcontactai.com/api/account/do-not-text", {
  method: "PUT",
  headers: {
    "Authorization": "Bearer <YOUR_API_KEY>",
    "Content-Type": "application/json",
    "Accept": "*/*"
  },
  body: JSON.stringify({
    clientId: "<YOUR_CLIENT_ID>",
    contactId: "your-contact-id",
    doNotText: false
  })
});

const data = await response.json();
console.log(`Contact ${data.contactId} do not text removed: ${data.doNotText}`);
```

### cURL Example

```bash
curl -X PUT "https://core.cloudcontactai.com/api/account/do-not-text" \
  -H "Authorization: Bearer <YOUR_API_KEY>" \
  -H "Content-Type: application/json" \
  -H "Accept: */*" \
  -d '{
    "clientId": "<YOUR_CLIENT_ID>",
    "contactId": "your-contact-id",
    "doNotText": true
  }'
```
