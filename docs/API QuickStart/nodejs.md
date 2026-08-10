---
title: Node.JS
excerpt: >-
  Send SMS, MMS, and Email with the CCAI Node.js SDK. Manage A2P 10DLC
  compliance, webhooks, and campaigns programmatically.
deprecated: false
hidden: false
metadata:
  title: Send emails, SMS, and MMS with Node.js - CloudContactAI
  description: >-
    Learn how to send your first email, SMS, and MMS using the CloudContactAI
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
<div style={{ margin: "16px 0 -8px 0" }}>
  <a
    href="https://app.cloudcontactai.com/register"
    style={{
      display: "inline-flex",
      alignItems: "center",
      justifyContent: "center",
      gap: "8px",
      backgroundColor: "#2563eb",
      color: "#ffffff",
      padding: "12px 20px",
      borderRadius: "12px",
      fontSize: "15px",
      fontWeight: 600,
      lineHeight: 1,
      textDecoration: "none",
      whiteSpace: "nowrap",
    }}
  >
    🔑 Get API Key
  </a>
</div>

Learn how to send your first SMS using the CCAI Node.js SDK

## Prerequisites

* Sign up for a [CCAI Trial Account](https://app.cloudcontactai.com/register)
* Get your **Client ID** from Account → Settings
* Create/Copy an **API Key** from Account Settings
* Node.js 16+ installed

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />

## 1. Install & Configuration

Install the SDK

```text
npm install ccai-node
```

### Environment Variables (Recommended)

Create a `.env` file in your project root:

```node
CCAI_CLIENT_ID=your-client-id
CCAI_API_KEY=your-api-key
```

Install dotenv:

```bash
npm install dotenv
```

### Initialize the Client

```javascript
import { CCAI } from 'ccai-node';
import 'dotenv/config';

const ccai = new CCAI({
  clientId: process.env.CCAI_CLIENT_ID,
  apiKey: process.env.CCAI_API_KEY
});
```

> **Security Note:** Never hardcode credentials in source files. Always use environment variables or a secrets manager.

***

## 2. Send SMS

### Single SMS

```javascript
ccai.sms.sendSingle(
  "Jane",
  "Smith",
  "+15559876543",
  "Hi ${firstName}, thanks for your interest!",
  "Single Message Test"
)
  .then(response => console.log('Success:', response))
  .catch(error => console.error('Error:', error));
```

### Bulk SMS / Campaign

Send to multiple recipients in a single call:

```javascript
const accounts = [
  { firstName: "John", lastName: "Doe", phone: "+15551234567" },
  { firstName: "Jane", lastName: "Smith", phone: "+15559876543" },
  { firstName: "Bob", lastName: "Johnson", phone: "+15551112222" }
];

ccai.sms.send(
  accounts,
  "Hello ${firstName} ${lastName}, this is a campaign message!",
  "Bulk SMS Campaign"
)
  .then(response => console.log('Campaign sent:', response))
  .catch(error => console.error('Error:', error));
```

### SMS with Options

```javascript
const options = {
  timeout: 60,
  retries: 3,
  onProgress: (status) => console.log(`${new Date().toISOString()} - ${status}`)
};

ccai.sms.send(accounts, message, "Campaign Title", options)
  .then(response => console.log('Success:', response))
  .catch(error => console.error('Error:', error));
```

***

## 3. Send MMS

### Complete MMS Workflow (Single Step)

```javascript
const account = {
  firstName: "John",
  lastName: "Doe",
  phone: "+15551234567"
};

const options = {
  timeout: 60,
  onProgress: (status) => console.log(`Progress: ${status}`)
};

ccai.mms.sendWithImage(
  "path/to/your/image.jpg",
  "image/jpeg",
  [account],
  "Hello ${firstName}, check out this image!",
  "MMS Campaign Example",
  options
)
  .then(response => console.log(`MMS sent! Campaign ID: ${response.campaignId}`))
  .catch(error => console.error('Error:', error));
```

### Step-by-Step MMS Workflow

For more control over the upload process:

```javascript
// Step 1: Get a signed URL for uploading
const uploadResponse = await ccai.mms.getSignedUploadUrl("image.jpg", "image/jpeg");
const { signedS3Url, fileKey } = uploadResponse;

// Step 2: Upload the image to the signed URL
const uploadSuccess = await ccai.mms.uploadImageToSignedUrl(
  signedS3Url,
  "path/to/your/image.jpg",
  "image/jpeg"
);

if (uploadSuccess) {
  // Step 3: Send the MMS with the uploaded image
  const response = await ccai.mms.send(
    fileKey,
    accounts,
    "Hello ${firstName}, check out this image!",
    "MMS Campaign Example"
  );
  console.log(`MMS sent! Campaign ID: ${response.campaignId}`);
}
```

### Single MMS

```javascript
const response = await ccai.mms.sendSingle(
  "your-client-id/campaign/image.jpg",
  "John",
  "Doe",
  "+15551234567",
  "Hello ${firstName}, check out this image!",
  "MMS Campaign"
);
```

### Supported Media Types

| Content Type | Extension   |
| ------------ | ----------- |
| `image/jpeg` | .jpg, .jpeg |
| `image/png`  | .png        |
| `image/gif`  | .gif        |

***

## 4. Send Email

### Single Email

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

### Email Campaign (Multiple Recipients)

```javascript
const emailAccounts = [
  { firstName: "John", lastName: "Doe", email: "john@example.com" },
  { firstName: "Jane", lastName: "Smith", email: "jane@example.com" }
];

const campaign = {
  subject: "Monthly Newsletter",
  title: "July 2025 Newsletter",
  message: `
    <h1>Monthly Newsletter</h1>
    <p>Hello \${firstName},</p>
    <p>Here are our updates for this month...</p>
  `,
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

const options = {
  onProgress: (status) => console.log(`Progress: ${status}`)
};

const campaignResponse = await ccai.email.sendCampaign(campaign, options);
console.log(`Email campaign sent with ID: ${campaignResponse.id}`);
```

### Schedule an Email Campaign

```javascript
const tomorrow = new Date();
tomorrow.setDate(tomorrow.getDate() + 1);
tomorrow.setHours(10, 0, 0, 0);

const scheduledCampaign = {
  subject: "Upcoming Event Reminder",
  title: "Event Reminder Campaign",
  message: `
    <h1>Reminder: Upcoming Event</h1>
    <p>Hello \${firstName},</p>
    <p>This is a reminder about our upcoming event tomorrow.</p>
  `,
  senderEmail: "events@yourcompany.com",
  replyEmail: "reply@yourcompany.com",
  senderName: "Your Company Events",
  accounts: emailAccounts,
  scheduledTimestamp: tomorrow.toISOString(),
  scheduledTimezone: "America/New_York"
};

const scheduledResponse = await ccai.email.sendCampaign(scheduledCampaign);
console.log(`Email campaign scheduled with ID: ${scheduledResponse.id}`);
```

***

## 5. Short Links

Create trackable short links for your campaigns:

```javascript
// Create a short link
const shortLink = await ccai.shortlink.create(
  "https://www.yourcompany.com/promo?utm_source=sms",
  "Summer Promo Link"
);

console.log(`Short URL: ${shortLink.url}`);
console.log(`Link ID: ${shortLink.id}`);

// Use in an SMS campaign
ccai.sms.send(
  accounts,
  `Hi \${firstName}, check out our summer deals: ${shortLink.url}`,
  "Summer Promo Campaign"
);
```

***

## 6. Voice

```javascript
// Send a voice message
const response = await ccai.voice.send(
  accounts,
  "Hello, this is a reminder about your appointment tomorrow at 3 PM.",
  "Appointment Reminder"
);

console.log(`Voice campaign sent: ${response.campaignId}`);
```

***

## 7. Conversations & Inbox

### Retrieve Conversation History

```javascript
// Get conversation history for a phone number
const conversations = await ccai.inbox.getConversation("+15551234567");

conversations.forEach(msg => {
  console.log(`[${msg.direction}] ${msg.timestamp}: ${msg.message}`);
});
```

### Manage Inbox State

```javascript
// Get inbox messages
const inbox = await ccai.inbox.list();

inbox.forEach(thread => {
  console.log(`From: ${thread.from}, Last Message: ${thread.lastMessage}`);
});
```

***

## 8. A2P 10DLC Compliance

### Brand Registration

Register your brand for A2P 10DLC compliance:

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

console.log(`Brand ID: ${brand.brandId}`);
console.log(`Brand Status: ${brand.status}`);
```

### Campaign Registration

After brand approval, register your messaging campaign:

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

### Check Registration Status

Poll for approval status:

```javascript
// Check brand status
const brandStatus = await ccai.compliance.getBrandStatus(brand.brandId);
console.log(`Brand Status: ${brandStatus.status}`); // PENDING, APPROVED, REJECTED

// Check campaign status
const campaignStatus = await ccai.compliance.getCampaignStatus(campaign.campaignId);
console.log(`Campaign Status: ${campaignStatus.status}`); // PENDING, APPROVED, REJECTED

// Poll until approved
async function waitForApproval(brandId, intervalMs = 30000) {
  let status = 'PENDING';
  while (status === 'PENDING') {
    const result = await ccai.compliance.getBrandStatus(brandId);
    status = result.status;
    if (status === 'PENDING') {
      console.log('Still pending, checking again in 30s...');
      await new Promise(resolve => setTimeout(resolve, intervalMs));
    }
  }
  return status;
}
```

***

## 9. Contact Validator

Validate email addresses and phone numbers.

> Bulk endpoints accept up to 50 contacts per request and are processed server-side in chunks.

```javascript
import { CCAI } from 'ccai-node';
import 'dotenv/config';

const ccai = new CCAI({
  clientId: process.env.CCAI_CLIENT_ID,
  apiKey: process.env.CCAI_API_KEY
});

// Validate a single email
const emailResult = await ccai.contactValidator.validateEmail('user@example.com');
console.log(emailResult.status); // "valid" | "invalid" | "risky"

// Validate multiple emails (up to 50)
const bulkEmails = await ccai.contactValidator.validateEmails([
  'user@example.com',
  'bad@invalid.xyz'
]);
console.log(`Total: ${bulkEmails.summary.total}`); // 2
console.log(`Valid: ${bulkEmails.summary.valid}`);  // 1

// Validate a single phone number
const phoneResult = await ccai.contactValidator.validatePhone('+15551234567', 'US');
console.log(phoneResult.status); // "valid" | "invalid" | "landline"

// Validate multiple phone numbers (up to 50)
const bulkPhones = await ccai.contactValidator.validatePhones([
  { phone: '+15551234567' },
  { phone: '+15559876543', countryCode: 'US' }
]);
console.log(`Landline: ${bulkPhones.summary.landline}`); // 1
```

***

## 10. Webhook Management

### Register a Webhook

```javascript
const webhookConfig = {
  url: "https://your-webhook-endpoint.com/webhook",
  events: ["MESSAGE_SENT", "MESSAGE_RECEIVED"],
  secret: "your-webhook-secret"
};

const registration = await ccai.webhook.register(webhookConfig);
console.log(`Webhook registered with ID: ${registration.id}`);
```

### List Webhooks

```javascript
const webhooks = await ccai.webhook.list();
webhooks.forEach(wh => {
  console.log(`Webhook ID: ${wh.id}, URL: ${wh.url}`);
});
```

### Update a Webhook

```javascript
const updatedWebhook = await ccai.webhook.update(registration.id, {
  url: "https://your-updated-endpoint.com/webhook",
  events: ["MESSAGE_SENT"],
  secret: "your-updated-secret"
});
```

### Delete a Webhook

```javascript
const deleteResponse = await ccai.webhook.delete(registration.id);
console.log(`Webhook deleted: ${deleteResponse.success}`);
```

### Webhook Event Types

| Event              | Description                        |
| ------------------ | ---------------------------------- |
| `DELIVERY_RECEIPT` | Message delivery status update     |
| `INBOUND_MESSAGE`  | Incoming message received          |
| `OPT_OUT`          | Contact opted out of messaging     |
| `MESSAGE_SENT`     | Outbound message sent successfully |
| `MESSAGE_RECEIVED` | Inbound message received           |

### Webhook Event Payloads

**Delivery Receipt:**

```json
{
  "message": "Hello John! We are testing the CCAI SMS functionality",
  "segments": 1,
  "smsSid": 141321,
  "messageStatus": "SENT",
  "totalPrice": 0.03,
  "to": "+15551234567"
}
```

**Inbound Message:**

```json
{
  "campaign": {
    "id": 141293,
    "title": "Default Campaign",
    "message": "",
    "senderPhone": null,
    "createdAt": "2025-08-13T21:20:50.212623Z",
    "runAt": "null"
  },
  "from": "+15551234567",
  "to": "+14158735045",
  "message": "Reply text here"
}
```

### Verify Webhook Signatures

Validate that incoming webhooks are genuinely from CCAI:

```javascript
import express from 'express';
import crypto from 'crypto';

const app = express();
app.use(express.json());

function verifyWebhookSignature(payload, signature, secret) {
  const expectedSignature = crypto
    .createHmac('sha256', secret)
    .update(JSON.stringify(payload))
    .digest('hex');
  return crypto.timingSafeEqual(
    Buffer.from(signature),
    Buffer.from(expectedSignature)
  );
}

app.post('/webhook', (req, res) => {
  const signature = req.headers['x-ccai-signature'];
  const secret = process.env.WEBHOOK_SECRET;

  if (!verifyWebhookSignature(req.body, signature, secret)) {
    return res.status(401).json({ error: 'Invalid signature' });
  }

  // Process the event
  const event = req.body;
  console.log('Received event:', event);

  if (event.messageStatus) {
    console.log(`Delivery receipt: ${event.messageStatus} for ${event.to}`);
  } else if (event.from && event.message) {
    console.log(`Inbound message from ${event.from}: ${event.message}`);
  }

  res.status(200).json({ received: true });
});

app.listen(3000, () => console.log('Webhook server running on port 3000'));
```

***

## 11. Testing Webhooks with Ngrok

### Step 1: Install Ngrok

```bash
brew install ngrok
```

### Step 2: Create a Webhook Server

```javascript
// webhook-server.js
import express from 'express';
import 'dotenv/config';

const app = express();
app.use(express.json());

app.post('/webhook', (req, res) => {
  console.log('Received webhook event!');
  console.log('Headers:', JSON.stringify(req.headers, null, 2));
  console.log('Body:', JSON.stringify(req.body, null, 2));
  res.status(200).json({ received: true });
});

app.listen(3000, () => {
  console.log('Webhook server listening on http://localhost:3000');
});
```

### Step 3: Start the Server

```bash
node webhook-server.js
```

### Step 4: Start Ngrok

In a separate terminal:

```bash
ngrok http 3000
```

Copy the `https://xxxxx.ngrok-free.app` URL from the output.

### Step 5: Configure CCAI

1. Log in to your CCAI account
2. Navigate to **Settings → Integration**
3. Set your webhook URLs:
   * Inbound message callback: `https://xxxxx.ngrok-free.app/webhook`
   * Outbound delivery callback: `https://xxxxx.ngrok-free.app/webhook`

### Step 6: Send a Test Message

```javascript
import { CCAI } from 'ccai-node';
import 'dotenv/config';

const ccai = new CCAI({
  clientId: process.env.CCAI_CLIENT_ID,
  apiKey: process.env.CCAI_API_KEY
});

await ccai.sms.sendSingle(
  "John",
  "Doe",
  "+15551234567",
  "Hello ${firstName}! Testing webhooks.",
  "Webhook Test"
);
```

Your webhook server should receive the delivery notification.

***

## 12. Error Handling

### Error Structure

```javascript
try {
  const response = await ccai.sms.sendSingle(
    "John", "Doe", "+15551234567",
    "Test message", "Test"
  );
} catch (error) {
  console.error(`Error Code: ${error.code}`);
  console.error(`Message: ${error.message}`);
  console.error(`Status: ${error.status}`);
  console.error(`Details: ${JSON.stringify(error.details)}`);
}
```

### Common Error Codes

| Code    | Description                          | Resolution                              |
| ------- | ------------------------------------ | --------------------------------------- |
| `40001` | Invalid API key                      | Verify your API key in Account Settings |
| `40002` | Invalid request parameters           | Check required fields and data formats  |
| `40003` | Rate limit exceeded                  | Implement exponential backoff           |
| `40004` | Insufficient credits                 | Add credits to your account             |
| `40101` | Authentication failed                | Verify clientId and apiKey              |
| `40301` | Forbidden - insufficient permissions | Check account permissions               |
| `40401` | Resource not found                   | Verify the resource ID exists           |
| `42201` | Invalid phone number format          | Use E.164 format (+1XXXXXXXXXX)         |
| `42202` | Recipient opted out                  | Remove contact from campaign            |
| `50001` | Internal server error                | Retry with exponential backoff          |

### Retry with Exponential Backoff

```javascript
async function sendWithRetry(fn, maxRetries = 3) {
  for (let attempt = 0; attempt <= maxRetries; attempt++) {
    try {
      return await fn();
    } catch (error) {
      if (attempt === maxRetries || error.code === 40101) {
        throw error;
      }
      const delay = Math.pow(2, attempt) * 1000;
      console.log(`Attempt ${attempt + 1} failed, retrying in ${delay}ms...`);
      await new Promise(resolve => setTimeout(resolve, delay));
    }
  }
}

// Usage
const response = await sendWithRetry(() =>
  ccai.sms.sendSingle("John", "Doe", "+15551234567", "Hello!", "Test")
);
```

***

## 13. Complete Module Reference

### SMS Module (`ccai.sms`)

| Method                                                             | Description                     |
| ------------------------------------------------------------------ | ------------------------------- |
| `send(accounts, message, title, options?)`                         | Send SMS to multiple recipients |
| `sendSingle(firstName, lastName, phone, message, title, options?)` | Send SMS to one recipient       |

### MMS Module (`ccai.mms`)

| Method                                                                      | Description                          |
| --------------------------------------------------------------------------- | ------------------------------------ |
| `sendWithImage(imagePath, contentType, accounts, message, title, options?)` | Upload and send MMS in one step      |
| `send(pictureFileKey, accounts, message, title, options?)`                  | Send MMS with pre-uploaded image     |
| `sendSingle(pictureFileKey, firstName, lastName, phone, message, title)`    | Send MMS to one recipient            |
| `getSignedUploadUrl(fileName, fileType)`                                    | Get a signed S3 URL for image upload |
| `uploadImageToSignedUrl(signedUrl, filePath, contentType)`                  | Upload image to signed URL           |

### Email Module (`ccai.email`)

| Method                                                                                                 | Description                                |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------ |
| `sendSingle(firstName, lastName, email, subject, message, senderEmail, replyEmail, senderName, title)` | Send email to one recipient                |
| `sendCampaign(campaign, options?)`                                                                     | Send email campaign to multiple recipients |

### Voice Module (`ccai.voice`)

| Method                                     | Description                               |
| ------------------------------------------ | ----------------------------------------- |
| `send(accounts, message, title, options?)` | Send voice message to multiple recipients |

### Short Link Module (`ccai.shortlink`)

| Method               | Description                   |
| -------------------- | ----------------------------- |
| `create(url, title)` | Create a trackable short link |

### Inbox Module (`ccai.inbox`)

| Method                   | Description                           |
| ------------------------ | ------------------------------------- |
| `list()`                 | List inbox threads                    |
| `getConversation(phone)` | Get conversation history for a number |

### Webhook Module (`ccai.webhook`)

| Method                                        | Description                     |
| --------------------------------------------- | ------------------------------- |
| `register(config)`                            | Register a new webhook endpoint |
| `list()`                                      | List all registered webhooks    |
| `update(id, config)`                          | Update an existing webhook      |
| `delete(id)`                                  | Delete a webhook                |
| `verifySignature(signature, payload, secret)` | Verify webhook signature        |
| `parseEvent(json)`                            | Parse a webhook event payload   |

### Compliance Module (`ccai.compliance`)

| Method                           | Description                        |
| -------------------------------- | ---------------------------------- |
| `registerBrand(brandData)`       | Register a brand for A2P 10DLC     |
| `registerCampaign(campaignData)` | Register a messaging campaign      |
| `getBrandStatus(brandId)`        | Check brand registration status    |
| `getCampaignStatus(campaignId)`  | Check campaign registration status |

***

## 14. Options Object Reference

### SMSOptions / MMSOptions

```javascript
{
  timeout: 60,          // Request timeout in seconds
  retries: 3,           // Number of retry attempts
  onProgress: (status) => {}  // Progress callback function
}
```

### EmailOptions

```javascript
{
  onProgress: (status) => {}  // Progress callback function
}
```

***

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/CloudContactAI/ccai-node/blob/main/LICENSE) file for details.

## Resources

* [GitHub Repository](https://github.com/CloudContactAI/ccai-node)
* [API Reference](https://developer.cloudcontactai.com/reference)
* [CCAI Dashboard](https://app.cloudcontactai.com)

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
