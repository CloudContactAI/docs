---
title: C#
excerpt: Send SMS with C#
deprecated: false
hidden: false
metadata:
  robots: index
---
Learn how to send your first SMS using the CCAI C# SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Paid Plan
* Create an API Key

## 1. Install

Get the CCAI Node.js SDK

```node
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

## 3. Try it yourself

See the full source code [here](https://github.com/CloudContactAI/CCAI.NET).