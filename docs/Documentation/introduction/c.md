---
title: C#
excerpt: Send SMS with C#
deprecated: false
hidden: false
metadata:
  title: Send emails, SMS, and MMS with C# - CloudContactAI
  description: >-
    Learn how to send your first email, SMS, and MMS using the CloudContactAI C#
    SDK
  image: >-
    https://files.readme.io/a5190d507936a4d6cf838dbf1d065aeacb7db8c29867dfcffb47e319cf32827d-Group_14.png
  keywords:
    - email
    - mms
    - sms
    - api
    - C#
  robots: index
---
Learn how to send your first SMS using the CCAI C# SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Trial Account [here](https://app.cloudcontactai.com/register)
* Get your Client ID from Account\Settings
* Create\Copy an API Key from Account Settings

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />

## 1. Install

Get the CCAI C# SDK

```text
dotnet add package CloudContactAI.CCAI.NET
```

## 2. Send SMS message

```csharp
using CCAI.NET;
using CCAI.NET.SMS;

// Initialize the client
var config = new CCAIConfig
{
    ClientId = "YOUR-CLIENT-ID",
    ApiKey = "YOUR-API-KEY"
};

using var ccai = new CCAIClient(config);

// Send a single SMS
var response = await ccai.SMS.SendSingleAsync(
    firstName: "John",
    lastName: "Doe",
    phone: "+15551234567",
    message: "Hello ${FirstName}, this is a test message!",
    title: "Test Campaign"
);

Console.WriteLine($"Message sent with ID: {response.Id}");

// Send to multiple recipients
var accounts = new List<Account>
{
    new Account
    {
        FirstName = "John",
        LastName = "Doe",
        Phone = "+15551234567"
    },
    new Account
    {
        FirstName = "Jane",
        LastName = "Smith",
        Phone = "+15559876543"
    }
};

var campaignResponse = await ccai.SMS.SendAsync(
    accounts: accounts,
    message: "Hello ${FirstName} ${LastName}, this is a test message!",
    title: "Bulk Test Campaign"
);

Console.WriteLine($"Campaign sent with ID: {campaignResponse.CampaignId}");
```

## 3. Email Usage

```csharp
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

## 4. Scheduling an Email

```csharp
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

## 5. Webhook Management

### CloudContact Webhook Events (New Format)

CloudContact now sends webhook notifications with a consistent structure for all event types:

```csharp
using CCAI.NET;
using CCAI.NET.Webhook;

// Parse CloudContact webhook event
var cloudContactEvent = ccai.Webhook.ParseCloudContactEvent(json);

switch (cloudContactEvent.EventType)
{
    case "message.sent":
        Console.WriteLine($"✅ Message delivered to {cloudContactEvent.Data.To}");
        Console.WriteLine($"   Cost: ${cloudContactEvent.Data.TotalPrice}");
        Console.WriteLine($"   Segments: {cloudContactEvent.Data.Segments}");
        break;
        
    case "message.incoming":
        Console.WriteLine($"📨 Reply from {cloudContactEvent.Data.From}: {cloudContactEvent.Data.Message}");
        break;
        
    case "message.excluded":
        Console.WriteLine($"⚠️ Message excluded: {cloudContactEvent.Data.ExcludedReason}");
        break;
        
    case "message.error.carrier":
        Console.WriteLine($"❌ Carrier error {cloudContactEvent.Data.ErrorCode}: {cloudContactEvent.Data.ErrorMessage}");
        break;
        
    case "message.error.cloudcontact":
        Console.WriteLine($"🚨 System error {cloudContactEvent.Data.ErrorCode}: {cloudContactEvent.Data.ErrorMessage}");
        break;
}
```

<br />

<br />

## &#x20;Try it yourself

See the full source code [here](https://github.com/CloudContactAI/CCAI.NET).
