---
title: Webhooks
deprecated: false
hidden: false
metadata:
  robots: index
---
> Use webhooks to notify your application about SMS and email events.

## What is a webhook?

A webhook is a way for CloudContactAI to notify your application in real time when specific events occur. Instead of having your app repeatedly check for updates, CloudContactAI sends the data to you automatically as soon as something happens. All webhooks use HTTPS and deliver a JSON payload that can be used by your application. You can use webhook feeds to do things like:

* Receive outbound SMS delivery notifications
* Receive incoming SMS message notifications

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

**ERROR:** Sign up for an account: [https://dashboard.ngrok.com/signup](https://dashboard.ngrok.com/signup)\
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

**SMS Callbacks:**

* Call this URL when an inbound message is received: `https://81dbae920588.ngrok-free.app/webhook`
* Call this URL after an outbound message has been delivered: `https://81dbae920588.ngrok-free.app/webhook`

<Image align="center" src="https://files.readme.io/9738d378d124c3eeeaba01ef47e20b07abbf146f9c6717e8b27f644c315e61ea-sms_callbacks.jpg" />

### Step 7: Send a test SMS to trigger webhook notification in Terminal 3

```bash
cd /Users/../CCAI.NET/examples
dotnet run
```

### Step 8: The Web server should receive the delivery notification

Press Ctrl+C to stop the server

```
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: http://localhost:3000
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Production
info: Microsoft.Hosting.Lifetime[0]
      Content root path: /Users/../CCAI.NET/examples/webhook-server
info: Microsoft.AspNetCore.Hosting.Diagnostics[1]
      Request starting HTTP/1.1 POST http://81dbae920588.ngrok-free.app/webhook - application/json 175
info: Microsoft.AspNetCore.Routing.EndpointMiddleware[0]
      Executing endpoint 'HTTP: POST /webhook'
Received webhook event at /webhook path!
Headers:
  Accept: application/json, application/*+json
  Host: 81dbae920589.ngrok-free.app
  User-Agent: Java/14-ea
  Accept-Encoding: gzip
  Content-Type: application/json
  Content-Length: 175
  X-Forwarded-For: 157.245.236.180
  X-Forwarded-Host: 81dbae920589.ngrok-free.app
  X-Forwarded-Proto: https
Body:
{"message":"Hello John! We are testing the CCAI SMS functionality with the webhooks","segments":1,"smsSid":141321,"messageStatus":"SENT","totalPrice":0.03,"to":"+1XXXYYYZZZZ"}
info: Microsoft.AspNetCore.Http.Result.OkObjectResult[1]
      Setting HTTP status code 200.
info: Microsoft.AspNetCore.Http.Result.OkObjectResult[3]
      Writing value of type 'String' as Json.
info: Microsoft.AspNetCore.Routing.EndpointMiddleware[1]
      Executed endpoint 'HTTP: POST /webhook'
info: Microsoft.AspNetCore.Hosting.Diagnostics[2]
      Request finished HTTP/1.1 POST http://81dbae920589.ngrok-free.app/webhook - 200 - application/json;+charset=utf-8 137.6141ms
```

### Step 9: From your phone, respond to the message

On your mobile phone, respond to the message that was sent to you by CCAI

### Step 10: Web Server should receive the response notification

```
Received webhook event at /webhook path!
Headers:
  Accept: text/plain, application/json, application/*+json, */*
  Host: 81dbae920589.ngrok-free.app
  User-Agent: Java/14-ea
  Accept-Encoding: gzip
  Content-Type: application/json
  Content-Length: 204
  X-Forwarded-For: 157.245.236.180
  X-Forwarded-Host: 81dbae920589.ngrok-free.app
  X-Forwarded-Proto: https
Body:
{"campaign":{"id":141293,"title":"Default Campaign","message":"","senderPhone":null,"createdAt":"2025-08-13T21:20:50.212623Z","runAt":"null"},"from":"+1XXXYYYZZZZ","to":"+14158735045","message":"Rockin "}
info: Microsoft.AspNetCore.Http.Result.OkObjectResult[1]
      Setting HTTP status code 200.
info: Microsoft.AspNetCore.Http.Result.OkObjectResult[3]
      Writing value of type 'String' as Json.
info: Microsoft.AspNetCore.Routing.EndpointMiddleware[1]
      Executed endpoint 'HTTP: POST /webhook'
info: Microsoft.AspNetCore.Hosting.Diagnostics[2]
      Request finished HTTP/1.1 POST http://81dbae920588.ngrok-free.app/webhook - 200 - application/json;+charset=utf-8 3.7664ms
```

This demonstrates a complete webhook testing workflow where:

1. Outbound SMS messages trigger delivery notifications
2. Inbound SMS responses trigger message received notifications
3. All webhook events are captured and logged by your local webhook server