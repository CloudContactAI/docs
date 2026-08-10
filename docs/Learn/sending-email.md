---
title: Sending Email
excerpt: >-
  Send transactional and marketing emails through CloudContactAI using your verified domain.
deprecated: false
hidden: false
metadata:
  title: Send Email with CloudContactAI | Email API for Business
  description: Learn how to send transactional and marketing emails with CloudContactAI. Send single emails, bulk campaigns, and scheduled email messages programmatically.
  keywords:
    - email
    - send email
    - email API
    - email campaigns
    - CloudContactAI
  robots: index
---

> Send transactional and marketing emails through CloudContactAI using your verified domain.

## Overview

CloudContactAI supports sending both transactional emails (order confirmations, password resets, notifications) and marketing emails (newsletters, promotions, drip campaigns). All emails are sent through Amazon SES via your verified domain, ensuring high deliverability.

## Prerequisites

Before sending email, you need to:

1. [Configure your email domain](https://developer.cloudcontactai.com/docs/configure-email-domain) with Amazon SES
2. Verify your sending domain in CloudContactAI
3. Have your API key and Client ID ready

## Email Types

### Transactional Email

One-to-one emails triggered by a specific action (e.g., a user signs up, places an order, or resets a password). These are time-sensitive and expected by the recipient.

**Examples:**
- Welcome emails
- Order confirmations
- Password reset links
- Account notifications

### Marketing Email

Bulk emails sent to a list of opted-in contacts for promotional or informational purposes.

**Examples:**
- Newsletters
- Product announcements
- Promotional offers
- Event invitations

## Sending a Single Email

Use the SDK to send a single transactional email:

```javascript
import { CCAI } from 'ccai-node';

const ccai = new CCAI({
  clientId: process.env.CCAI_CLIENT_ID,
  apiKey: process.env.CCAI_API_KEY
});

const response = await ccai.email.sendSingle(
  "John",                              // First name
  "Doe",                               // Last name
  "john@example.com",                  // Recipient email
  "Welcome to Our Service",            // Subject
  "<p>Hello ${firstName},</p><p>Thank you for signing up!</p>",  // HTML body
  "noreply@yourcompany.com",           // Sender email
  "reply@yourcompany.com",             // Reply-to email
  "Your Company",                      // Sender name
  "Welcome Email"                      // Campaign title
);

console.log(`Email sent with ID: ${response.id}`);
```

## Sending an Email Campaign

Send to multiple recipients in a single call:

```javascript
const emailAccounts = [
  { firstName: "John", lastName: "Doe", email: "john@example.com" },
  { firstName: "Jane", lastName: "Smith", email: "jane@example.com" }
];

const campaign = {
  subject: "Monthly Newsletter",
  title: "July Newsletter",
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

const response = await ccai.email.sendCampaign(campaign);
console.log(`Email campaign sent with ID: ${response.id}`);
```

## Scheduling an Email

Schedule an email campaign to send at a future time:

```javascript
const tomorrow = new Date();
tomorrow.setDate(tomorrow.getDate() + 1);
tomorrow.setHours(10, 0, 0, 0);

const scheduledCampaign = {
  subject: "Upcoming Event Reminder",
  title: "Event Reminder Campaign",
  message: "<p>Hello ${firstName},</p><p>Reminder about our event tomorrow.</p>",
  senderEmail: "events@yourcompany.com",
  replyEmail: "reply@yourcompany.com",
  senderName: "Your Company Events",
  accounts: emailAccounts,
  scheduledTimestamp: tomorrow.toISOString(),
  scheduledTimezone: "America/New_York"
};

const response = await ccai.email.sendCampaign(scheduledCampaign);
console.log(`Email campaign scheduled with ID: ${response.id}`);
```

## Dynamic Variables

Use `${variableName}` syntax in your email subject and body to personalize content:

| Variable | Description |
|----------|-------------|
| `${firstName}` | Recipient's first name |
| `${lastName}` | Recipient's last name |
| `${email}` | Recipient's email address |

## HTML Email Best Practices

- Use inline CSS styles (many email clients strip `<style>` blocks)
- Keep email width under 600px for mobile compatibility
- Include a plain-text fallback when possible
- Always include an unsubscribe link in marketing emails
- Test rendering across major email clients (Gmail, Outlook, Apple Mail)

## Deliverability Tips

- Only send to contacts who have explicitly opted in
- Keep your bounce rate below 2%
- Keep your complaint rate below 0.1%
- Warm up new sending domains gradually
- Use a consistent "From" address
- Authenticate your domain with SPF, DKIM, and DMARC

## Related Pages

- [Configure Email Domain](https://developer.cloudcontactai.com/docs/configure-email-domain) - Set up Amazon SES
- [Register Email Domain](https://developer.cloudcontactai.com/docs/register-email-domain) - Verify your domain with CCAI
- [Multi-Domain Email](https://developer.cloudcontactai.com/docs/multi-domain-email) - Send from multiple domains
