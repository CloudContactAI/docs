---
title: Register Campaign
excerpt: >-
  Register your messaging campaign for A2P 10DLC compliance after brand approval with CloudContactAI.
deprecated: false
hidden: false
metadata:
  title: A2P 10DLC Campaign Registration | CloudContactAI Compliance API
  description: Register your SMS messaging campaign for A2P 10DLC compliance using the CloudContactAI SDK. Define your use case, message samples, and opt-in flow programmatically.
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
- Sample messages that represent your campaign's content
- A defined opt-in flow describing how contacts consent to receive messages

## Register Your Campaign

Use the CloudContactAI SDK to submit your campaign registration programmatically.

**Endpoint:**

```
POST https://core.cloudcontactai.com/api/compliance/campaigns
```

**JavaScript (SDK):**

```javascript
const campaign = await ccai.compliance.registerCampaign({
  brandId: brand.brandId,
  useCase: "MARKETING",
  description: "Promotional messages for opted-in customers",
  messageFlow: "Customers opt-in via web form and receive promotional SMS",
  sampleMessages: [
    "Hi ${firstName}, check out our latest deals at https://example.com",
    "Your order #12345 has shipped! Track it here: https://example.com/track"
  ],
  helpMessage: "Reply HELP for assistance. Contact support@yourcompany.com",
  optOutMessage: "You have been unsubscribed. Reply START to re-subscribe."
});

console.log(`Campaign ID: ${campaign.campaignId}`);
console.log(`Campaign Status: ${campaign.status}`);
```

**cURL:**

```bash
curl -X POST https://core.cloudcontactai.com/api/compliance/campaigns \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "brandId": "BRAND_abc123",
    "useCase": "MARKETING",
    "description": "Promotional messages for opted-in customers",
    "messageFlow": "Customers opt-in via web form and receive promotional SMS",
    "sampleMessages": [
      "Hi ${firstName}, check out our latest deals at https://example.com",
      "Your order #12345 has shipped! Track it here: https://example.com/track"
    ],
    "helpMessage": "Reply HELP for assistance. Contact support@yourcompany.com",
    "optOutMessage": "You have been unsubscribed. Reply START to re-subscribe."
  }'
```

## Request Parameters

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `brandId` | string | Yes | The brand ID from your approved brand registration |
| `useCase` | string | Yes | The campaign use case type (see options below) |
| `description` | string | Yes | A clear description of what your campaign does |
| `messageFlow` | string | Yes | How contacts opt in and what messages they receive |
| `sampleMessages` | array | Yes | 2-5 sample messages representative of your campaign content |
| `helpMessage` | string | Yes | The message sent when a contact replies HELP |
| `optOutMessage` | string | Yes | The message sent when a contact opts out |

### Supported Use Cases

- `MARKETING` - Promotional content, sales, and offers
- `TRANSACTIONAL` - Order confirmations, shipping updates, account alerts
- `CUSTOMER_CARE` - Support replies and service notifications
- `ACCOUNT_NOTIFICATION` - Password resets, verification codes, account updates
- `DELIVERY_NOTIFICATION` - Delivery status and logistics updates
- `FRAUD_ALERT` - Security and fraud detection alerts
- `MIXED` - Combination of multiple use cases
- `POLLING_AND_VOTING` - Surveys, polls, and feedback requests
- `PUBLIC_SERVICE_ANNOUNCEMENT` - Non-commercial public information

## Response

```json
{
  "campaignId": "CAMP_xyz789",
  "brandId": "BRAND_abc123",
  "useCase": "MARKETING",
  "status": "PENDING",
  "createdAt": "2026-08-10T15:30:00Z"
}
```

## Best Practices for Approval

- **Be specific in your description.** Vague descriptions like "sending messages" are more likely to be rejected.
- **Sample messages should be realistic.** Include actual dynamic variables and URLs you plan to use.
- **Clearly describe your opt-in flow.** Carriers want to see that contacts explicitly consent to receive messages.
- **Include HELP and STOP handling.** Both are required for compliance.
- **Match your use case to your content.** Do not register as TRANSACTIONAL if you are sending marketing messages.

## What Happens Next

After submitting your campaign registration:

1. Your campaign enters a **PENDING** state for review
2. Review typically takes 1 to 5 business days
3. Once approved, your campaign is active and messages will benefit from improved throughput
4. If rejected, review the rejection reason and resubmit with corrections

Use the [Check Registration Status](https://developer.cloudcontactai.com/docs/check-registration-status) endpoint to monitor your campaign approval.
