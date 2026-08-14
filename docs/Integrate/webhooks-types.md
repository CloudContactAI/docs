---
title: Webhook Event Types
deprecated: false
hidden: false
metadata:
  robots: index
---
CloudContactAI sends webhook notifications to your configured endpoint when specific events occur in your account. All events follow a consistent structure with an `eventType` and `data` object containing event information.

## Webhook Configuration

Configure your webhook URL in the CloudContactAI dashboard under **Client Settings > Webhooks**. All event types will be sent to the same endpoint using the HTTP method you specify (POST or PUT).

## Event Types

### message.sent

**Description:** Triggered when a message is successfully sent from CloudContactAI to a contact.

**When it's sent:**

- Message has been sent to the Contact.
- Occurs for both individual messages and campaign messages
- Includes pricing and segmentation information

**JSON Example:**

```json
{
  "eventType": "message.sent",
  "data": {
    "SmsSid": 12345,
    "MessageStatus": "DELIVERED",
    "To": "+1234567890",
    "Message": "Hello! Your order #12345 has been shipped.",
    "CustomData": "order_id:12345,customer_type:premium",
    "ClientExternalId": "customer_abc123",
    "CampaignId": 67890,
    "CampaignTitle": "Order Notifications",
    "Segments": 2,
    "TotalPrice": 0.02
  }
}
```

***

### message.incoming

**Description:** Triggered when a recipient replies to one of your messages or sends a message to your CloudContactAI phone number.

**When it's sent:**

- Message received from external phone number
- Processed through CloudContactAI's incoming message system
- Contact is not blocked from sending messages

**JSON Example:**

```json
{
  "eventType": "message.incoming",
  "data": {
    "SmsSid": 0,
    "MessageStatus": "RECEIVED",
    "To": "+0987654321",
    "Message": "Yes, I'm interested in learning more!",
    "CustomData": "",
    "ClientExternalId": "customer_abc123",
    "CampaignId": 67890,
    "CampaignTitle": "Lead Generation Campaign",
    "From": "+1234567890"
  }
}
```

***

### message.excluded

**Description:** Triggered when a message is excluded from being sent during campaign creation due to filtering rules.

**When it's sent:**

- Contact matches exclusion criteria (duplicate phone, invalid format, etc.)
- The exclusion process occurs prior to the processing of the campaign before messages are sent.
- Helps track why certain contacts didn't receive messages

**JSON Example:**

```json
{
  "eventType": "message.excluded",
  "data": {
    "SmsSid": 0,
    "MessageStatus": "EXCLUDED",
    "To": "+1234567890",
    "Message": "Hi {{name}}, check out our new products!",
    "CustomData": "lead_source:website,segment:new_users",
    "ClientExternalId": "customer_xyz789",
    "CampaignId": 67890,
    "CampaignTitle": "Product Launch Campaign",
    "ExcludedReason": "Duplicate phone number in campaign"
  }
}
```

**Common Exclusion Reasons:**

- "Duplicate phone number in campaign"
- "Invalid phone number format"
- "Contact opted out"
- "Phone number blacklisted"

***

### message.error.carrier

**Description:** Triggered when a message fails to be delivered due to carrier specific errors.

**When it's sent:**

- Carrier returns an error status for the message
- Network or carrier-specific delivery failures
- Invalid destination numbers or carrier restrictions

**JSON Example:**

```json
{
  "eventType": "message.error.carrier",
  "data": {
    "SmsSid": 12345,
    "MessageStatus": "FAILED",
    "To": "+1234567890",
    "Message": "Your verification code is: 123456",
    "CustomData": "verification_attempt:1",
    "ClientExternalId": "user_def456",
    "CampaignId": 0,
    "CampaignTitle": "",
    "ErrorCode": "30008",
    "ErrorMessage": "Unknown destination handset",
    "ErrorType": "carrier"
  }
}
```

**Common Carrier Error Codes:**

- `30008`: Unknown destination handset
- `30007`: Message delivery failed
- `21211`: Invalid 'To' phone number
- `21614`: 'To' number is not a valid mobile number

***

### message.error.cloudcontact

**Description:** Triggered when a message fails due to internal CloudContactAI system errors.

**When it's sent:**

- Internal processing errors (CCAI- prefixed error codes)
- System configuration issues
- Account or subscription related problems

**JSON Example:**

```json
{
  "eventType": "message.error.cloudcontact",
  "data": {
    "SmsSid": 12345,
    "MessageStatus": "FAILED",
    "To": "+1234567890",
    "Message": "Welcome to our service!",
    "CustomData": "signup_source:landing_page",
    "ClientExternalId": "new_user_ghi789",
    "CampaignId": 67890,
    "CampaignTitle": "Welcome Series",
    "ErrorCode": "CCAI-001",
    "ErrorMessage": "Insufficient account balance",
    "ErrorType": "cloudcontact"
  }
}
```

**Common CloudContactAI Error Codes:**

- `CCAI-001`: Insufficient account balance
- `CCAI-002`: Account suspended
- `CCAI-003`: Message quota exceeded
- `CCAI-004`: Invalid campaign configuration

***

### contact.unsubscribed

**Description:** Triggered when an incoming message is received with some of this texts (_cancel, end, quit, stop, stopall, unsubscribe_) and the contact will be flagged as "do not text".

**When it's sent:**

- Message received from external phone number with text cancel, stop, etc.
- Contact is flagged as do not text manually
- AI prompts checking the incoming message and decide to flag as do not text

**JSON Example:**

```json
{
  "eventType": "contact.unsubscribed",
  "data": {
    "id": 0,
    "MessageStatus": "DO_NOT_TEXT",
    "To": "+0987654321",
    "Message": "STOP",
    "CustomData": "",
    "ClientExternalId": "customer_abc123",
    "CampaignId": 67890,
    "CampaignTitle": "Lead Generation Campaign",
    "UnsubscribedAt": "2025-09-25T11:08:14.368388Z",
    "ContactData": {
      "firstName": "Jon",
      "lastName": "Doe",
      "email": null,
      "phone": "+0997654321"
    }
  }
}
```

***

### email.delivered

**Description:** Triggered when an email is successfully delivered to the recipient's mail server, as confirmed by AWS SES or SendGrid.

**When it's sent:**

- AWS SES or SendGrid reports a successful delivery event for a campaign email
- Fires after the email status has been updated in the CloudContactAI database

**JSON Example:**

```json
{
  "eventType": "email.delivered",
  "data": {
    "clientId": 12345,
    "campaignId": 67890,
    "emailMessageId": 111222,
    "toEmail": "recipient@example.com",
    "fromEmail": "sender@client.com",
    "subject": "Your Monthly Statement",
    "timestamp": "2026-08-12T23:15:00Z"
  }
}
```

**Field Reference:**

| Field            | Type           | Description                                                      |
| ---------------- | -------------- | ---------------------------------------------------------------- |
| `clientId`       | number         | Your CloudContactAI client ID                                    |
| `campaignId`     | number \| null | The ID of the email campaign                                     |
| `emailMessageId` | number         | The internal ID of the individual email message                  |
| `toEmail`        | string \| null | The recipient email address                                      |
| `fromEmail`      | string \| null | The sender email address                                         |
| `subject`        | string \| null | The email subject line                                           |
| `timestamp`      | string         | ISO-8601 timestamp of the delivery event from the email provider |

***

### email.bounced

**Description:** Triggered when an email bounces — either a hard bounce (permanent delivery failure) or a soft bounce (temporary failure) — as reported by AWS SES or SendGrid.

**When it's sent:**

- AWS SES or SendGrid reports a bounce event for a campaign email
- Fires after the email status has been updated in the CloudContactAI database

**JSON Example:**

```json
{
  "eventType": "email.bounced",
  "data": {
    "clientId": 12345,
    "campaignId": 67890,
    "emailMessageId": 111222,
    "toEmail": "recipient@example.com",
    "fromEmail": "sender@client.com",
    "subject": "Your Monthly Statement",
    "timestamp": "2026-08-12T23:15:00Z",
    "bounceType": "Permanent",
    "bounceSubType": "General"
  }
}
```

**Field Reference:**

| Field            | Type           | Description                                     |
| ---------------- | -------------- | ----------------------------------------------- |
| `clientId`       | number         | Your CloudContactAI client ID                   |
| `campaignId`     | number \| null | The ID of the email campaign                    |
| `emailMessageId` | number         | The internal ID of the individual email message |
| `toEmail`        | string \| null | The recipient email address                     |
| `fromEmail`      | string \| null | The sender email address                        |
| `subject`        | string \| null | The email subject line                          |
| `timestamp`      | string         | ISO-8601 timestamp of the bounce event          |
| `bounceType`     | string         | The bounce category (see values below)          |
| `bounceSubType`  | string         | The bounce sub-category (see values below)      |

`bounceType`**&#x20;Values:**

| Value          | Description                                                                |
| -------------- | -------------------------------------------------------------------------- |
| `Permanent`    | Hard bounce — the email address does not exist or permanently rejects mail |
| `Transient`    | Soft bounce — temporary failure such as a full mailbox                     |
| `Undetermined` | The bounce type could not be determined                                    |

`bounceSubType`**&#x20;Values:**

| Value                      | Description                                            |
| -------------------------- | ------------------------------------------------------ |
| `General`                  | An unspecified bounce reason                           |
| `NoEmail`                  | The email address does not exist                       |
| `Suppressed`               | The address is on a suppression list                   |
| `OnAccountSuppressionList` | The address is on the account-level suppression list   |
| `MailboxFull`              | The recipient's mailbox is full                        |
| `MessageTooLarge`          | The message exceeded the recipient server's size limit |
| `ContentRejected`          | The content of the message was rejected                |
| `AttachmentRejected`       | An attachment in the message was rejected              |

***

### email.complaint

**Description:** Triggered when a recipient marks your email as spam, as reported by AWS SES or SendGrid.

**When it's sent:**

- AWS SES or SendGrid reports a complaint/spam-report event for a campaign email
- Fires after the email status has been updated in the CloudContactAI database

**JSON Example:**

```json
{
  "eventType": "email.complaint",
  "data": {
    "clientId": 12345,
    "campaignId": 67890,
    "emailMessageId": 111222,
    "toEmail": "recipient@example.com",
    "fromEmail": "sender@client.com",
    "subject": "Your Monthly Statement",
    "timestamp": "2026-08-12T23:15:00Z",
    "complaintFeedbackType": "abuse"
  }
}
```

**Field Reference:**

| Field                   | Type           | Description                                     |
| ----------------------- | -------------- | ----------------------------------------------- |
| `clientId`              | number         | Your CloudContactAI client ID                   |
| `campaignId`            | number \| null | The ID of the email campaign                    |
| `emailMessageId`        | number         | The internal ID of the individual email message |
| `toEmail`               | string \| null | The recipient email address                     |
| `fromEmail`             | string \| null | The sender email address                        |
| `subject`               | string \| null | The email subject line                          |
| `timestamp`             | string         | ISO-8601 timestamp of the complaint event       |
| `complaintFeedbackType` | string         | The type of spam complaint (see values below)   |

`complaintFeedbackType`**&#x20;Values (from AWS SES ARF):**

| Value          | Description                                                          |
| -------------- | -------------------------------------------------------------------- |
| `abuse`        | The recipient reported the message as spam or unsolicited            |
| `auth-failure` | The message failed email authentication checks                       |
| `fraud`        | The message was identified as fraudulent                             |
| `not-spam`     | The recipient marked the message as not spam (false positive report) |
| `other`        | Unspecified complaint type                                           |
| `virus`        | The message contained a virus or malware                             |

> **Note:** When the complaint originates from SendGrid, the `complaintFeedbackType` is always `"abuse"`.

***

### email.unsubscribed

**Description:** Triggered when a contact clicks the unsubscribe link in one of your emails.

**When it's sent:**

- A recipient clicks the unsubscribe link embedded in a campaign email
- The contact is marked as unsubscribed from email communications in CloudContactAI

**JSON Example:**

```json
{
  "eventType": "email.unsubscribed",
  "data": {
    "clientId": 12345,
    "contactId": "abc-123",
    "toEmail": "recipient@example.com",
    "unsubscribeMethod": "link_click",
    "timestamp": "2026-08-12T23:15:00Z"
  }
}
```

**Field Reference:**

| Field               | Type           | Description                                                                                                |
| ------------------- | -------------- | ---------------------------------------------------------------------------------------------------------- |
| `clientId`          | number         | Your CloudContactAI client ID                                                                              |
| `contactId`         | string         | The CloudContactAI contact identifier                                                                      |
| `toEmail`           | string \| null | The email address of the contact who unsubscribed. May be `null` if no email is on record for the contact. |
| `unsubscribeMethod` | string         | The method used to unsubscribe. Currently always `"link_click"`.                                           |
| `timestamp`         | string         | ISO-8601 timestamp of the unsubscribe action                                                               |

> **Note:** Unlike other email events, `email.unsubscribed` does not include `campaignId`, `emailMessageId`, `fromEmail`, or `subject`. The unsubscribe link contains a contact-level token and does not reference a specific campaign message.
