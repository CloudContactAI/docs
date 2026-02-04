---
title: Node.js
excerpt: Send SMS with Node.js
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

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Trial Account [here](https://app.cloudcontactai.com/register)
* Get your Client ID from Account\Settings
* Create\Copy an API Key from Account Settings

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />

## 1. Install

Get the CCAI Node.js SDK

```text
npm install ccai-node
```

## 2. Send SMS message

```node
import { CCAI } from 'ccai-node';

// Initialize the client
const ccai = new CCAI({
  clientId: 'YOUR-CLIENT-ID',
  apiKey: 'API-KEY-TOKEN'
});

// Send an SMS to multiple recipients
const accounts = [
  {
    firstName: "John",
    lastName: "Doe",
    phone: "+15551234567"
  }
];

ccai.sms.send(
  accounts,
  "Hello ${firstName} ${lastName}, this is a test message!",
  "Test Campaign"
)
  .then(response => console.log('Success:', response))
  .catch(error => console.error('Error:', error));

// Send an SMS to a single recipient
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

## 3. Send MMS

```node
using CCAI.NET;
using CCAI.NET.SMS;
using DotNetEnv;

// Load environment variables
Env.Load();

// Initialize the client
var config = new CCAIConfig
{
    ClientId = Environment.GetEnvironmentVariable("CCAI_CLIENT_ID") ?? throw new InvalidOperationException("CCAI_CLIENT_ID not found"),
    ApiKey = Environment.GetEnvironmentVariable("CCAI_API_KEY") ?? throw new InvalidOperationException("CCAI_API_KEY not found")
};

using var ccai = new CCAIClient(config);

// Create options with progress tracking
var options = new SMSOptions
{
    Timeout = 60,
    OnProgress = status => Console.WriteLine($"Progress: {status}")
};

// Complete MMS workflow (get URL, upload image, send MMS)
var imagePath = "path/to/your/image.jpg";
var contentType = "image/jpeg";

// Define recipient
var account = new Account
{
    FirstName = "John",
    LastName = "Doe",
    Phone = "+15551234567"  // Use E.164 format
};

// Send MMS with image in one step
var response = await ccai.MMS.SendWithImageAsync(
    imagePath: imagePath,
    contentType: contentType,
    accounts: new[] { account },
    message: "Hello ${FirstName}, check out this image!",
    title: "MMS Campaign Example",
    options: options
);

Console.WriteLine($"MMS sent! Campaign ID: {response.CampaignId}");
```

## 4. Send Email

```node
using CCAI.NET;
using CCAI.NET.Email;
using DotNetEnv;

// Load environment variables
Env.Load();

// Initialize the client
var config = new CCAIConfig
{
    ClientId = Environment.GetEnvironmentVariable("CCAI_CLIENT_ID") ?? throw new InvalidOperationException("CCAI_CLIENT_ID not found"),
    ApiKey = Environment.GetEnvironmentVariable("CCAI_API_KEY") ?? throw new InvalidOperationException("CCAI_API_KEY not found")
};

using var ccai = new CCAIClient(config);

// Send a single email
var response = await ccai.Email.SendSingleAsync(
    firstName: "John",
    lastName: "Doe",
    email: "john@example.com",
    subject: "Welcome to Our Service",
    message: "<p>Hello ${FirstName},</p><p>Thank you for signing up!</p>",
    senderEmail: "noreply@yourcompany.com",
    replyEmail: "support@yourcompany.com",
    senderName: "Your Company",
    title: "Welcome Email"
);

Console.WriteLine($"Email sent with ID: {response.Id}");

// Send to multiple recipients
var emailAccounts = new List<EmailAccount>
{
    new EmailAccount
    {
        FirstName = "John",
        LastName = "Doe",
        Email = "john@example.com"
    },
    new EmailAccount
    {
        FirstName = "Jane",
        LastName = "Smith",
        Email = "jane@example.com"
    }
};

var campaign = new EmailCampaign
{
    Subject = "Monthly Newsletter",
    Title = "July 2025 Newsletter",
    Message = @"
        <h1>Monthly Newsletter - July 2025</h1>
        <p>Hello ${FirstName},</p>
        <p>Here are our updates for this month...</p>
    ",
    SenderEmail = "newsletter@yourcompany.com",
    ReplyEmail = "support@yourcompany.com",
    SenderName = "Your Company Newsletter",
    Accounts = emailAccounts,
    CampaignType = "EMAIL",
    AddToList = "noList",
    ContactInput = "accounts",
    FromType = "single",
    Senders = new List<object>()
};

var campaignResponse = await ccai.Email.SendCampaignAsync(
    campaign: campaign,
    options: new EmailOptions
    {
        OnProgress = status => Console.WriteLine($"Progress: {status}")
    }
);

Console.WriteLine($"Email campaign sent with ID: {campaignResponse.Id}");
```

## 5. Schedule an Email Campaign

```node
// Schedule for tomorrow at 10:00 AM
var tomorrow = DateTime.Now.AddDays(1).Date.AddHours(10);

var scheduledCampaign = new EmailCampaign
{
    Subject = "Upcoming Event Reminder",
    Title = "Event Reminder Campaign",
    Message = @"
        <h1>Reminder: Upcoming Event</h1>
        <p>Hello ${FirstName},</p>
        <p>This is a reminder about our upcoming event tomorrow.</p>
    ",
    SenderEmail = "events@yourcompany.com",
    ReplyEmail = "events@yourcompany.com",
    SenderName = "Your Company Events",
    Accounts = emailAccounts,
    ScheduledTimestamp = tomorrow.ToString("o"), // ISO 8601 format
    ScheduledTimezone = "America/New_York"
};

var scheduledResponse = await ccai.Email.SendCampaignAsync(scheduledCampaign);
Console.WriteLine($"Email campaign scheduled with ID: {scheduledResponse.Id}");
```

## 6. Webhook Management

```node
using CCAI.NET;
using CCAI.NET.Webhook;
using DotNetEnv;

// Load environment variables
Env.Load();

// Initialize the client
var config = new CCAIConfig
{
    ClientId = Environment.GetEnvironmentVariable("CCAI_CLIENT_ID") ?? throw new InvalidOperationException("CCAI_CLIENT_ID not found"),
    ApiKey = Environment.GetEnvironmentVariable("CCAI_API_KEY") ?? throw new InvalidOperationException("CCAI_API_KEY not found")
};

using var ccai = new CCAIClient(config);

// Register a webhook
var webhookConfig = new WebhookConfig
{
    Url = "https://your-webhook-endpoint.com/webhook",
    Events = new List<WebhookEventType>
    {
        WebhookEventType.MessageSent,
        WebhookEventType.MessageReceived
    },
    Secret = "your-webhook-secret"
};

var registration = await ccai.Webhook.RegisterAsync(webhookConfig);
Console.WriteLine($"Webhook registered with ID: {registration.Id}");

// List all webhooks
var webhooks = await ccai.Webhook.ListAsync();
foreach (var webhook in webhooks)
{
    Console.WriteLine($"Webhook ID: {webhook.Id}, URL: {webhook.Url}");
}

// Update a webhook
var updatedConfig = new WebhookConfig
{
    Url = "https://your-updated-endpoint.com/webhook",
    Events = new List<WebhookEventType> { WebhookEventType.MessageSent },
    Secret = "your-updated-secret"
};

var updatedWebhook = await ccai.Webhook.UpdateAsync(registration.Id, updatedConfig);

// Delete a webhook
var deleteResponse = await ccai.Webhook.DeleteAsync(registration.Id);
Console.WriteLine($"Webhook deleted: {deleteResponse.Success}");

// Parse a webhook event (in your webhook handler)
public void ProcessWebhookEvent(string json, string signature, string secret)
{
    // Verify the signature
    if (ccai.Webhook.VerifySignature(signature, json, secret))
    {
        // Parse the event
        var webhookEvent = ccai.Webhook.ParseEvent(json);
        
        if (webhookEvent is MessageSentEvent sentEvent)
        {
            Console.WriteLine($"Message sent to: {sentEvent.To}");
        }
        else if (webhookEvent is MessageReceivedEvent receivedEvent)
        {
            Console.WriteLine($"Message received from: {receivedEvent.From}");
        }
    }
    else
    {
        Console.WriteLine("Invalid signature");
    }
}
```

## 7. Step-by-Step MMS Workflow

```node
// Step 1: Get a signed URL for uploading
var uploadResponse = await ccai.MMS.GetSignedUploadUrlAsync(
    fileName: "image.jpg",
    fileType: "image/jpeg"
);

var signedUrl = uploadResponse.SignedS3Url;
var fileKey = uploadResponse.FileKey;

// Step 2: Upload the image to the signed URL
var uploadSuccess = await ccai.MMS.UploadImageToSignedUrlAsync(
    signedUrl: signedUrl,
    filePath: "path/to/your/image.jpg",
    contentType: "image/jpeg"
);

if (uploadSuccess)
{
    // Step 3: Send the MMS with the uploaded image
    var response = await ccai.MMS.SendAsync(
        pictureFileKey: fileKey,
        accounts: accounts,
        message: "Hello ${FirstName}, check out this image!",
        title: "MMS Campaign Example"
    );
    
    Console.WriteLine($"MMS sent! Campaign ID: {response.CampaignId}");
}
```

## 8. With Tracking Process

```node
// Create options with progress tracking
var options = new SMSOptions
{
    Timeout = 60,
    Retries = 3,
    OnProgress = status => Console.WriteLine($"{DateTime.Now:yyyy-MM-dd HH:mm:ss} - {status}")
};

// Send SMS with progress tracking
var response = await ccai.SMS.SendAsync(
    accounts: accounts,
    message: message,
    title: title,
    options: options
);
```

## 9. Synchronous API

```node
// Send a single SMS synchronously
var response = ccai.SMS.SendSingle(
    firstName: "John",
    lastName: "Doe",
    phone: "+15551234567",
    message: "Hello ${FirstName}, this is a test message!",
    title: "Test Campaign"
);

// Send a single MMS synchronously
var mmsResponse = ccai.MMS.SendSingle(
    pictureFileKey: "your-client-id/campaign/image.jpg",
    firstName: "John",
    lastName: "Doe",
    phone: "+15551234567",
    message: "Hello ${FirstName}, check out this image!",
    title: "MMS Campaign"
);

// Send a single email synchronously
var emailResponse = ccai.Email.SendSingle(
    firstName: "John",
    lastName: "Doe",
    email: "john@example.com",
    subject: "Welcome to Our Service",
    message: "<p>Hello ${FirstName},</p><p>Thank you for signing up!</p>",
    senderEmail: "noreply@yourcompany.com",
    replyEmail: "support@yourcompany.com",
    senderName: "Your Company",
    title: "Welcome Email"
);
```

### License

This project is licensed under the MIT License - see the [LICENSE ](https://github.com/CloudContactAI/ccai-node/blob/main/LICENSE)file for details.

## &#x20;Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-node).

## 10. Testing Webhook Installation

### Step 1: Install Ngrok

```
brew install ngrok
```

### Step 2: Verify Ngrok

```
ngrok version
```

### Step 3: Start the standalone webhook server

Open a new terminal window and run:

```
cd /Users/../CCAI.NET/examples/webhook-server
dotnet run
```

This will start a webhook server on [http://localhost:3000](http://localhost:3000)

### Step 4: In another terminal, start Ngrok

Open another terminal window and run:

```
ngrok http 3000
```

This will create a public tunnel to your local webhook server.

If you have not signed up for ngrok, you will need to:

ERROR: Sign up for an account: [https://dashboard.ngrok.com/signup](https://dashboard.ngrok.com/signup)
ERROR: Install your authtoken: [https://dashboard.ngrok.com/get-started/your-authtoken](https://dashboard.ngrok.com/get-started/your-authtoken)

### Step 5: Get your ngrok URL

Ngrok will display something like:

Forwarding    [https://abc123.ngrok.io](https://abc123.ngrok.io) -> [http://localhost:3000](http://localhost:3000)
Copy that [https://abc123.ngrok.io](https://abc123.ngrok.io) URL - this is your public webhook URL.

Example: [https://81dbae920588.ngrok-free.app](https://81dbae920588.ngrok-free.app)

### Step 6: Configure CCAI with your Ngrok URL

1. Log in to your CCAI account
2. Navigate to the Settings\Integration tab
3. Specify your ngrok url + '/webhook'
4. SMS Callbacks:

Call this URL when an inbound message is received: [https://81dbae920588.ngrok-free.app/webhook](https://81dbae920588.ngrok-free.app/webhook)
Call this URL after an outbound message has been delivered: [https://81dbae920588.ngrok-free.app/webhook](https://81dbae920588.ngrok-free.app/webhook)

### Step 7: Send a test SMS to trigger webhook

```
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
      Content root path: /Users/j../CCAI.NET/examples/webhook-server
info: Microsoft.AspNetCore.Hosting.Diagnostics[1]
      Request starting HTTP/1.1 POST http://81dbae920588.ngrok-free.app/webhook - application/json 175
info: Microsoft.AspNetCore.Routing.EndpointMiddleware[0]
      Executing endpoint 'HTTP: POST /webhook'
Received webhook event at /webhook path!
Headers:
  Accept: application/json, application/*+json
  Host: 81dbae920588.ngrok-free.app
  User-Agent: Java/14-ea
  Accept-Encoding: gzip
  Content-Type: application/json
  Content-Length: 175
  X-Forwarded-For: 157.245.236.180
  X-Forwarded-Host: 81dbae920588.ngrok-free.app
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
Request finished HTTP/1.1 POST http://81dbae920588.ngrok-free.app/webhook - 200 - application/json;+charset=utf-8 137.6141m

```

### Step 9: Respond to the message on your phone

On your mobile phone, respond to the message that was sent to you by CCAI

### Step 10: Web Server should receive your response notice

```
Received webhook event at /webhook path!
Headers:
  Accept: text/plain, application/json, application/*+json, */*
  Host: 81dbae920588.ngrok-free.app
  User-Agent: Java/14-ea
  Accept-Encoding: gzip
  Content-Type: application/json
  Content-Length: 204
  X-Forwarded-For: 157.245.236.180
  X-Forwarded-Host: 81dbae920588.ngrok-free.app
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

<br />

## &#x20;Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-node).
