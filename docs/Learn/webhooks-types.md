---
title: Webhooks Types
deprecated: false
hidden: false
metadata:
  robots: index
---
CloudContact sends webhook notifications to your configured endpoint when specific events occur in your account. All events follow a consistent structure with an `eventType` and `data` object containing event information.

## Webhook Configuration

Configure your webhook URL in the CloudContact dashboard under **Client Settings > Webhooks**. All event types will be sent to the same endpoint using the HTTP method you specify (POST or PUT).

## Event Types

### message.sent

**Description:** Triggered when a message is successfully sent from CloudContact to a recipient.

**When it's sent:**

* Message has been delivered to the carrier
* Occurs for both individual messages and campaign messages
* Includes pricing and segmentation information

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

**Description:** Triggered when a recipient replies to one of your messages or sends a message to your CloudContact phone number.

**When it's sent:**

* Message received from external phone number
* Processed through CloudContact's incoming message system
* Contact is not blocked from sending messages

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
    "From": "+1234567890",
    "To": "+0987654321"
  }
}
```

***

### message.excluded

**Description:** Triggered when a message is excluded from being sent during campaign creation due to filtering rules.

**When it's sent:**

* Contact matches exclusion criteria (duplicate phone, invalid format, etc.)
* Occurs during campaign processing before messages are sent
* Helps track why certain contacts didn't receive messages

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

* "Duplicate phone number in campaign"
* "Invalid phone number format"
* "Contact opted out"
* "Phone number blacklisted"

***

### message.error.carrier

**Description:** Triggered when a message fails to be delivered due to carrier-level errors.

**When it's sent:**

* Carrier returns an error status for the message
* Network or carrier-specific delivery failures
* Invalid destination numbers or carrier restrictions

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

* `30008`: Unknown destination handset
* `30007`: Message delivery failed
* `21211`: Invalid 'To' phone number
* `21614`: 'To' number is not a valid mobile number

***

### message.error.cloudcontact

**Description:** Triggered when a message fails due to internal CloudContact system errors.

**When it's sent:**

* Internal processing errors (CCAI- prefixed error codes)
* System configuration issues
* Account or subscription related problems

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

**Common CloudContact Error Codes:**

* `CCAI-001`: Insufficient account balance
* `CCAI-002`: Account suspended
* `CCAI-003`: Message quota exceeded
* `CCAI-004`: Invalid campaign configuration

***
