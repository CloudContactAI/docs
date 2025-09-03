---
title: Webhook
excerpt: >-
  A webhook is a way for CloudContactAI to notify your application in real time
  when specific events occur.
deprecated: false
hidden: false
metadata:
  title: CCAI SMS Webhook Notifications
  description: How to receive SMS Webhook Notifications in C#
  image: >-
    https://files.readme.io/304cbc299350d0a7df08b0aba4e2892f36638df288dff7b486a2cffe87ac855d-sms_callbacks.jpg
  keywords:
    - C$
    - webhook
    - SMS
    - notifications
  robots: index
---
> Use the CloudContactAI webhook to notify your application about SMS events.

## What is a webhook?

A webhook is a way for CloudContactAI to notify your application in real time when specific events occur. Instead of having your app repeatedly check for updates, CloudContactAI sends the data to you automatically as soon as something happens. All webhooks use HTTPS and deliver a JSON payload that can be used by your application.

You can use the CloudContactAI webhook to see the following things about your SMS messages:

* Sent - An outbound SMS message is sent successfully to a contact.
* Incoming - An inbound SMS message is received by a CloudContactAI phone number.
* Excluded - An outbound SMS message was excluded from being sent. This can take place for a number of different reasons, but the most common is that the user has unsubscribed from your CloudContactAI phone number.
* Error Carrier - An outbound message was not delivered to the contact due to a carrier-level error.
* Error CloudContactAI - An outbound message was not delivered due to an error with CloudContactAI. For example, your account has insufficient balance.

Details on the event types can be found [here](https://developer.cloudcontactai.com/docs/webhooks-types#/). []()

## Testing Webhook Installation

### Step 1: Install Ngrok

```bash
brew install ngrok
```

### Step 2: Verify Ngrok

```bash
ngrok version
```

### Step 3: Start the standalone webhook server in Terminal 1

Open a new terminal window and run:

```bash
cd /Users/../CCAI.NET/examples/webhook-server
dotnet run
```

This will start a webhook server on `http://localhost:3000`

### Step 4: In another terminal, start ngrok in Terminal 2

Open another terminal window and run:

```bash
ngrok http 3000
```

This will create a public tunnel to your local webhook server.

If you have not signed up for ngrok, you will need to:

**ERROR:** Sign up for an account: [https://dashboard.ngrok.com/signup](https://dashboard.ngrok.com/signup)
**ERROR:** Install your authtoken: [https://dashboard.ngrok.com/get-started/your-authtoken](https://dashboard.ngrok.com/get-started/your-authtoken)

### Step 5: Get your ngrok URL

ngrok will display something like:

```
Forwarding    https://abc123.ngrok.io -> http://localhost:3000
```

Copy that `https://abc123.ngrok.io` URL - this is your public webhook URL.

Example: `https://81dbae920588.ngrok-free.app`

### Step 6: Configure CCAI with your Ngrok URL

1. Log in to your CCAI account
2. Navigate to the Settings\Integration tab
3. Specify your ngrok url + '/webhook'

**Webhook URL:**`

![](https://files.readme.io/3b812ff9e7fa942aab01445000b247a2eb34d32ce7d7ae2783d79946506f99b5-image.png)

<br />

### Step 7: Send a test SMS to trigger webhook notification in Terminal 3

```bash
cd /Users/../CCAI.NET/examples
dotnet run
```

### Step 8: The Web server should receive the delivery notification

Press Ctrl+C to stop the server

```
🔔 Received webhook event at root path!
⏰ Time: 2025-09-03 00:51:19 UTC
📋 Headers:
  Accept: application/json, application/*+json
  Host: 13c29ec4a161.ngrok-free.app
  User-Agent: Java/14-ea
  Accept-Encoding: gzip
  Content-Type: application/json
  Content-Length: 304
  X-Forwarded-For: 159.65.99.19
  X-Forwarded-Host: 13c29ec4a161.ngrok-free.app
  X-Forwarded-Proto: https
📄 Raw Body:
{"eventType":"message.sent","data":{"id":142065,"MessageStatus":"SENT","To":"+14155551212","Message":"Hello John Doe, this is a test message!","CustomData":"","ClientExternalId":"a43c42c6-b0c1-45c5-b2fb-290ee7e6f113","CampaignId":141293,"CampaignTitle":"Default Campaign","Segments":1,"TotalPrice":0.03}}

🎯 Parsed CloudContact Event:
   Event Type: message.sent
   Message Status: SENT
   To: +14155551212
   Message: Hello John Doe, this is a test message!
   ✅ Message delivered successfully!
   💰 Cost: $0.0300
   📊 Segments: 1
   📢 Campaign: Default Campaign (ID: 141293)
   🆔 External ID: a43c42c6-b0c1-45c5-b2fb-290ee7e6f113application/json;+charset=utf-8 137.6141ms
```

### Step 9: This demonstrates a complete webhook testing workflow where:

1. Outbound SMS messages trigger delivery notifications
2. All webhook events are captured and logged by your local webhook server
