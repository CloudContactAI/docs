---
title: Register A2P 10DLC Campaign - API
excerpt: >-
  Register your messaging campaign for A2P 10DLC compliance after brand approval
  with CloudContactAI.
deprecated: false
hidden: false
metadata:
  title: A2P 10DLC Campaign Registration | CloudContactAI Compliance API
  description: >-
    Register your SMS messaging campaign for A2P 10DLC compliance using the
    CloudContactAI SDK. Define your use case, message samples, and opt-in flow
    programmatically.
  keywords:
    - A2P 10DLC
    - campaign registration
    - SMS compliance
    - messaging campaign
    - CloudContactAI
  robots: index
---

> Register your messaging campaign after brand approval to define your SMS use case and message flow.

## Overview

Campaign registration is the second step in A2P 10DLC compliance. After your brand is approved, you must register each messaging campaign to describe how you intend to use SMS. This tells carriers what type of messages you will send, how customers opt in, and what your messages look like.

## Prerequisites

- An approved brand registration (see [Register Brand](https://developer.cloudcontactai.com/docs/register-brand))
- Your brand ID from the brand registration response
- 2 to 5 sample messages that represent your campaign's content
- A defined opt-in flow describing how contacts consent to receive messages

## Register Your Campaign

**Base URL:** `https://compliance.cloudcontactai.com/api`

**Endpoint:**

```
POST /v1/campaigns
```

**JavaScript (SDK):**

```javascript
const campaign = await ccai.campaigns.create({
  brandId: 123,
  useCase: "MARKETING",
  description: "Promotional messages for opted-in customers",
  messageFlow: "Customers opt-in via web form and receive promotional SMS",
  hasEmbeddedLinks: true,
  hasEmbeddedPhone: false,
  isAgeGated: false,
  isDirectLending: false,
  optInKeywords: ["START", "YES"],
  optInMessage: "You are now subscribed to updates from Your Company. Reply STOP to unsubscribe, HELP for help.",
  optInProofUrl: "https://www.yourcompany.com/sms-opt-in",
  helpKeywords: ["HELP", "INFO"],
  helpMessage: "Reply HELP for assistance. Contact support@yourcompany.com or call 1-800-555-0123.",
  optOutKeywords: ["STOP", "CANCEL", "UNSUBSCRIBE"],
  optOutMessage: "You have been unsubscribed and will no longer receive messages. Reply START to re-subscribe.",
  sampleMessages: [
    "Hi Jane, check out our latest deals at https://example.com. Reply STOP to opt out.",
    "Your order #12345 has shipped! Track it here: https://example.com/track. Reply HELP for help."
  ]
});

console.log(`Campaign ID: ${campaign.id}`);
```

**cURL:**

```bash
curl -X POST https://compliance.cloudcontactai.com/api/v1/campaigns \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "brandId": 123,
    "useCase": "MARKETING",
    "description": "Promotional messages for opted-in customers",
    "messageFlow": "Customers opt-in via web form and receive promotional SMS",
    "hasEmbeddedLinks": true,
    "hasEmbeddedPhone": false,
    "isAgeGated": false,
    "isDirectLending": false,
    "optInKeywords": ["START", "YES"],
    "optInMessage": "You are now subscribed to updates from Your Company. Reply STOP to unsubscribe, HELP for help.",
    "optInProofUrl": "https://www.yourcompany.com/sms-opt-in",
    "helpKeywords": ["HELP", "INFO"],
    "helpMessage": "Reply HELP for assistance. Contact support@yourcompany.com or call 1-800-555-0123.",
    "optOutKeywords": ["STOP", "CANCEL", "UNSUBSCRIBE"],
    "optOutMessage": "You have been unsubscribed and will no longer receive messages. Reply START to re-subscribe.",
    "sampleMessages": [
      "Hi Jane, check out our latest deals at https://example.com. Reply STOP to opt out.",
      "Your order #12345 has shipped! Track it here: https://example.com/track. Reply HELP for help."
    ]
  }'
```

## Request Parameters

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `brandId` | integer | Yes | The brand ID from your approved brand registration |
| `useCase` | string | Yes | The campaign use case type (see options below) |
| `description` | string | Yes | A clear description of what your campaign does |
| `messageFlow` | string | Yes | How contacts opt in and what messages they receive |
| `hasEmbeddedLinks` | boolean | Yes | Whether messages contain URLs |
| `hasEmbeddedPhone` | boolean | Yes | Whether messages contain phone numbers |
| `isAgeGated` | boolean | Yes | Whether content is age-restricted |
| `isDirectLending` | boolean | Yes | Whether campaign involves direct lending |
| `optInKeywords` | array | Yes | Keywords that trigger opt-in (e.g., ["START", "YES"]) |
| `optInMessage` | string | Yes | Message sent when a contact opts in |
| `optInProofUrl` | string | Yes | URL showing your opt-in mechanism (must start with http:// or https://) |
| `helpKeywords` | array | Yes | Keywords that trigger help (e.g., ["HELP", "INFO"]) |
| `helpMessage` | string | Yes | Message sent when a contact replies with a help keyword |
| `optOutKeywords` | array | Yes | Keywords that trigger opt-out (e.g., ["STOP", "CANCEL"]) |
| `optOutMessage` | string | Yes | Message sent when a contact opts out (must contain "STOP" or one of your optOutKeywords) |
| `sampleMessages` | array | Yes | 2 to 5 sample messages representative of your campaign |
| `subUseCases` | array | Conditional | Required for MIXED/LOW_VOLUME_MIXED (2-3 sub use cases) |
| `termsLink` | string | No | URL to your terms of service |
| `privacyLink` | string | No | URL to your privacy policy |

### Supported Use Cases

- `TWO_FACTOR_AUTHENTICATION`
- `ACCOUNT_NOTIFICATION`
- `CUSTOMER_CARE`
- `DELIVERY_NOTIFICATION`
- `FRAUD_ALERT`
- `HIGHER_EDUCATION`
- `LOW_VOLUME_MIXED`
- `MARKETING`
- `MIXED`
- `POLLING_VOTING`
- `PUBLIC_SERVICE_ANNOUNCEMENT`
- `SECURITY_ALERT`

### Supported Sub Use Cases (for MIXED/LOW_VOLUME_MIXED)

- `TWO_FACTOR_AUTHENTICATION`
- `ACCOUNT_NOTIFICATION`
- `CUSTOMER_CARE`
- `DELIVERY_NOTIFICATION`
- `FRAUD_ALERT`
- `MARKETING`
- `POLLING_VOTING`

## Response

```json
{
  "id": 789,
  "accountId": 456,
  "brandId": 123,
  "useCase": "MARKETING",
  "description": "Promotional messages for opted-in customers",
  "messageFlow": "Customers opt-in via web form and receive promotional SMS",
  "monthlyFee": 10.00,
  "createdAt": "2026-08-10T15:30:00Z",
  "updatedAt": "2026-08-10T15:30:00Z"
}
```

## Other Campaign Endpoints

| Operation | Method | Endpoint |
|-----------|--------|----------|
| List campaigns | GET | `/v1/campaigns` |
| Get campaign | GET | `/v1/campaigns/{id}` |
| Update campaign | PATCH | `/v1/campaigns/{id}` |
| Delete campaign | DELETE | `/v1/campaigns/{id}` |

## Validation Rules

- `sampleMessages` must contain 2 to 5 items
- At least one sample message must contain "Reply STOP" or "Reply {optOutKeyword}"
- At least one sample message must contain "Reply HELP" or "Reply {helpKeyword}"
- `optOutMessage` must contain "STOP" or one of your `optOutKeywords`
- `helpMessage` must contain "HELP" or one of your `helpKeywords`
- `optInProofUrl`, `termsLink`, and `privacyLink` must start with `http://` or `https://`
- MIXED and LOW_VOLUME_MIXED use cases require 2 to 3 `subUseCases`

## What Happens Next

After submitting your campaign registration:

1. Your campaign is created and stored
2. Review typically takes 1 to 5 business days
3. Once approved, your campaign is active and messages will benefit from improved throughput
4. If rejected, review the rejection reason and resubmit with corrections

Use the [Check Registration Status](https://developer.cloudcontactai.com/docs/check-registration-status) endpoint to monitor your campaign approval.