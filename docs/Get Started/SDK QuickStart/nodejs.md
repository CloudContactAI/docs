---
title: Node.JS
excerpt: >-
  Send SMS, MMS, and Email with the CCAI Node.js SDK. Manage A2P 10DLC
  compliance, webhooks, and campaigns programmatically.
deprecated: false
hidden: false
metadata:
  title: Send SMS, MMS, and Email with Node.js - CloudContactAI
  description: >-
    Learn how to send your first SMS and Email using the CloudContactAI
    Node.js SDK
  image: >-
    https://files.readme.io/d0e3164cc01be24b9f6edfc8d999466a442c65fe9f98f999cc7e2b997cb9f88e-Group_14.png
  keywords:
    - email
    - sms
    - mms
    - node.js
    - api
  robots: index
---

## Prerequisites

- [Create an API Key](https://app.cloudcontactai.com/register) — you'll need your Client ID and API Key from Account → Settings
- [Acquire a Phone Number](/docs/phone-numbers) — required for SMS and MMS
- Node.js 16+ installed

<Steps>

<Step title="Install">

<CodeGroup>

```bash npm
npm install ccai-node
```

```bash yarn
yarn add ccai-node
```

```bash pnpm
pnpm add ccai-node
```

</CodeGroup>

</Step>

<Step title="Configure your credentials">

Create a `.env` file in your project root:

```bash
CCAI_CLIENT_ID=your-client-id
CCAI_API_KEY=your-api-key
```

Install dotenv if needed:

```bash
npm install dotenv
```

Then initialize the client:

```javascript
import { CCAI } from 'ccai-node';
import 'dotenv/config';

const ccai = new CCAI({
  clientId: process.env.CCAI_CLIENT_ID,
  apiKey: process.env.CCAI_API_KEY
});
```

> **Security note:** Never hardcode credentials in source files. Always use environment variables or a secrets manager.

</Step>

<Step title="Send your first SMS">

```javascript
const response = await ccai.sms.sendSingle(
  "Jane",
  "Smith",
  "+15559876543",
  "Hi ${firstName}, thanks for your interest!",
  "My First Message"
);

console.log('Sent:', response);
```

</Step>

<Step title="Send your first Email">

```javascript
const response = await ccai.email.sendSingle(
  "John",
  "Doe",
  "john@example.com",
  "Welcome to Our Service",
  "<p>Hello ${firstName},</p><p>Thank you for signing up!</p>",
  "noreply@yourcompany.com",
  "reply@yourcompany.com",
  "Your Company",
  "Welcome Email"
);

console.log(`Email sent with ID: ${response.id}`);
```

</Step>

</Steps>

## Examples

<Cards columns={3}>
  <Card title="Bulk SMS Campaign" href="https://github.com/CloudContactAI/ccai-node#bulk-sms--campaign" icon="fa-duotone fa-messages" />
  <Card title="Send MMS" href="https://github.com/CloudContactAI/ccai-node#send-mms" icon="fa-duotone fa-image" />
  <Card title="Email Campaign" href="https://github.com/CloudContactAI/ccai-node#email-campaign" icon="fa-duotone fa-envelope-open-text" />
  <Card title="Webhooks" href="https://github.com/CloudContactAI/ccai-node#webhook-management" icon="fa-duotone fa-webhook" />
  <Card title="A2P 10DLC Compliance" href="https://github.com/CloudContactAI/ccai-node#a2p-10dlc-compliance" icon="fa-duotone fa-shield-check" />
  <Card title="Contact Validator" href="https://github.com/CloudContactAI/ccai-node#contact-validator" icon="fa-duotone fa-address-book" />
  <Card title="Short Links" href="https://github.com/CloudContactAI/ccai-node#short-links" icon="fa-duotone fa-link" />
  <Card title="Voice" href="https://github.com/CloudContactAI/ccai-node#voice" icon="fa-duotone fa-phone" />
  <Card title="Conversations & Inbox" href="https://github.com/CloudContactAI/ccai-node#conversations--inbox" icon="fa-duotone fa-inbox" />
</Cards>

---

## Bulk SMS

Send to multiple recipients in a single call:

```javascript
const accounts = [
  { firstName: "John", lastName: "Doe", phone: "+15551234567" },
  { firstName: "Jane", lastName: "Smith", phone: "+15559876543" },
  { firstName: "Bob", lastName: "Johnson", phone: "+15551112222" }
];

const response = await ccai.sms.send(
  accounts,
  "Hello ${firstName} ${lastName}, this is a campaign message!",
  "Bulk SMS Campaign"
);

console.log('Campaign sent:', response);
```

---

## Send MMS

### One-step (upload + send)

```javascript
const response = await ccai.mms.sendWithImage(
  "path/to/your/image.jpg",
  "image/jpeg",
  [{ firstName: "John", lastName: "Doe", phone: "+15551234567" }],
  "Hello ${firstName}, check out this image!",
  "MMS Campaign Example"
);

console.log(`MMS sent! Campaign ID: ${response.campaignId}`);
```

### Step-by-step (manual upload)

```javascript
// Step 1: Get a signed upload URL
const { signedS3Url, fileKey } = await ccai.mms.getSignedUploadUrl("image.jpg", "image/jpeg");

// Step 2: Upload the image
await ccai.mms.uploadImageToSignedUrl(signedS3Url, "path/to/your/image.jpg", "image/jpeg");

// Step 3: Send MMS
const response = await ccai.mms.send(
  fileKey,
  accounts,
  "Hello ${firstName}, check out this image!",
  "MMS Campaign Example"
);
```

**Supported media types**

| Content Type | Extension |
| --- | --- |
| `image/jpeg` | .jpg, .jpeg |
| `image/png` | .png |
| `image/gif` | .gif |

---

## Email Campaign

```javascript
const emailAccounts = [
  { firstName: "John", lastName: "Doe", email: "john@example.com" },
  { firstName: "Jane", lastName: "Smith", email: "jane@example.com" }
];

const campaign = {
  subject: "Monthly Newsletter",
  title: "July 2025 Newsletter",
  message: `<h1>Monthly Newsletter</h1><p>Hello \${firstName}, here are this month's updates...</p>`,
  senderEmail: "newsletter@yourcompany.com",
  replyEmail: "reply@yourcompany.com",
  senderName: "Your Company Newsletter",
  accounts: emailAccounts,
  campaignType: "EMAIL",
  addToList: "noList",
  contactInput: "accounts",
  fromType: "single",
  senders: []
};

const campaignResponse = await ccai.email.sendCampaign(campaign);
console.log(`Campaign sent with ID: ${campaignResponse.id}`);
```

---

## Webhooks

### Register a webhook

```javascript
const registration = await ccai.webhook.register({
  url: "https://your-webhook-endpoint.com/webhook",
  events: ["MESSAGE_SENT", "MESSAGE_RECEIVED"],
  secret: "your-webhook-secret"
});

console.log(`Registered with ID: ${registration.id}`);
```

### Verify webhook signatures

```javascript
import crypto from 'crypto';

function verifyWebhookSignature(payload, signature, secret) {
  const expected = crypto
    .createHmac('sha256', secret)
    .update(JSON.stringify(payload))
    .digest('hex');
  return crypto.timingSafeEqual(Buffer.from(signature), Buffer.from(expected));
}
```

**Webhook event types**

| Event | Description |
| --- | --- |
| `DELIVERY_RECEIPT` | Message delivery status update |
| `INBOUND_MESSAGE` | Incoming message received |
| `OPT_OUT` | Contact opted out of messaging |
| `MESSAGE_SENT` | Outbound message sent successfully |
| `MESSAGE_RECEIVED` | Inbound message received |

---

## A2P 10DLC Compliance

### Register brand

```javascript
const brand = await ccai.compliance.registerBrand({
  legalName: "Your Company LLC",
  taxId: "12-3456789",
  taxIdCountry: "US",
  website: "https://www.yourcompany.com",
  vertical: "TECHNOLOGY",
  entityType: "PRIVATE_PROFIT",
  address: {
    street: "123 Main St",
    city: "San Francisco",
    state: "CA",
    postalCode: "94105",
    country: "US"
  },
  contactEmail: "compliance@yourcompany.com",
  contactPhone: "+14155551234"
});

console.log(`Brand ID: ${brand.brandId} — Status: ${brand.status}`);
```

### Register campaign

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
  helpMessage: "Reply HELP for assistance.",
  optOutMessage: "You have been unsubscribed. Reply START to re-subscribe."
});
```

---

## Contact Validator

```javascript
// Validate a single email
const emailResult = await ccai.contactValidator.validateEmail('user@example.com');
console.log(emailResult.status); // "valid" | "invalid" | "risky"

// Validate a single phone number
const phoneResult = await ccai.contactValidator.validatePhone('+15551234567', 'US');
console.log(phoneResult.status); // "valid" | "invalid" | "landline"

// Bulk validate (up to 50 per request)
const bulkResult = await ccai.contactValidator.validatePhones([
  { phone: '+15551234567' },
  { phone: '+15559876543', countryCode: 'US' }
]);
```

---

## Error Handling

```javascript
try {
  const response = await ccai.sms.sendSingle(
    "John", "Doe", "+15551234567", "Test message", "Test"
  );
} catch (error) {
  console.error(`[${error.code}] ${error.message}`);
}
```

**Common error codes**

| Code | Description | Resolution |
| --- | --- | --- |
| `40001` | Invalid API key | Verify your API key in Account Settings |
| `40002` | Invalid request parameters | Check required fields and data formats |
| `40003` | Rate limit exceeded | Implement exponential backoff |
| `40004` | Insufficient credits | Add credits to your account |
| `40101` | Authentication failed | Verify clientId and apiKey |
| `42201` | Invalid phone number format | Use E.164 format (+1XXXXXXXXXX) |
| `42202` | Recipient opted out | Remove contact from campaign |
| `50001` | Internal server error | Retry with exponential backoff |

---

## Resources

- [GitHub Repository](https://github.com/CloudContactAI/ccai-node)
- [API Reference](https://developer.cloudcontactai.com/reference)
- [CCAI Dashboard](https://app.cloudcontactai.com)

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "SoftwareSourceCode",
  "name": "ccai-node",
  "description": "Node.js SDK for CloudContactAI. Send SMS, MMS, and Email campaigns programmatically with webhook support.",
  "codeRepository": "https://github.com/CloudContactAI/ccai-node",
  "programmingLanguage": "JavaScript",
  "runtimePlatform": "Node.js",
  "license": "https://opensource.org/licenses/MIT",
  "author": {
    "@type": "Organization",
    "name": "CloudContactAI",
    "url": "https://cloudcontactai.com"
  }
}
</script>
