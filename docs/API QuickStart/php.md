---
title: PHP
excerpt: Send SMS or MMS with PHP
deprecated: false
hidden: false
metadata:
  title: Send emails, SMS, and MMS with PHP - CloudContactAI
  description: >-
    Learn how to send your first email, SMS, and MMS using the CloudContactAI
    PHP SDK
  image: >-
    https://files.readme.io/d1bab7924f7126429ffa5626418d89005171ccfcfc1b375c3fc4454a273bc716-Group_14.png
  keywords:
    - email
    - sms
    - mms
    - api
    - php
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

Learn how to send your first SMS using the CCAI PHP SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Trial Account [here](https://app.cloudcontactai.com/register)
* Get your Client ID from Account\Settings
* Create\Copy an API Key from Account Settings

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />

## 1. Install

Get the CCAI PHP SDK

```text
composer require cloudcontactai/ccai-php
```

## Configuration

You can configure the client using environmental variables:

```text
# Set your CCAI credentials as environment variables
export CCAI_CLIENT_ID="your-client-id"
export CCAI_API_KEY="your-api-key"
```

Or provide the code directly:

```
$ccai = new CCAI([
    'clientId' => 'YOUR-CLIENT-ID',
    'apiKey' => 'YOUR-API-KEY'
]);
```

<br />

## 2. Send SMS message

```node
<?php

require 'vendor/autoload.php';

use CloudContactAI\CCAI\CCAI;
use CloudContactAI\CCAI\SMS\Account;

// Initialize the client
$ccai = new CCAI([
    'clientId' => 'YOUR-CLIENT-ID',
    'apiKey' => 'YOUR-API-KEY'
]);

// Send a single SMS
$response = $ccai->sms->sendSingle(
    firstName: 'John',
    lastName: 'Doe',
    phone: '+15551234567',
    message: 'Hello ${firstName}, this is a test message!',
    title: 'Test Campaign'
);

echo "Message sent with ID: " . $response->id . "\n";

// Send to multiple recipients
$accounts = [
    new Account('John', 'Doe', '+15551234567'),
    new Account('Jane', 'Smith', '+15559876543')
];

$campaignResponse = $ccai->sms->send(
    accounts: $accounts,
    message: 'Hello ${firstName} ${lastName}, this is a test message!',
    title: 'Bulk Test Campaign'
);

echo "Campaign sent with ID: " . $campaignResponse->campaignId . "\n";
```

## 3. Send MMS Message

```php
<?php

/**
 * Simple example of sending an MMS message using the CCAI PHP library
 */

require_once __DIR__ . '/../vendor/autoload.php';

use CloudContactAI\CCAI\CCAI;

// Replace with your actual credentials
$ccai = new CCAI([
    'clientId' => getenv('CCAI_CLIENT_ID') ?: 'YOUR_CLIENT_ID',
    'apiKey' => getenv('CCAI_API_KEY') ?: 'YOUR_API_KEY'
]);

// Path to the image file you want to send
$filename = 'AllCode.png';
$imagePath = __DIR__ . '/AllCode.png';
$contentType = 'image/png';

try {
    // Send an MMS to a single recipient
    $response = $ccai->mms->sendWithImage(
        $imagePath,
        $contentType,
        [
            [
                'firstName' => 'Jane',
                'lastName' => 'Doe',
                'phone' => '+15555555555'
            ]
        ],
        'Hi ${firstName} ${lastName}, testing a new campaign',
        'MMS Content Test Message'
    );
    
    echo "MMS sent successfully! ID: " . $response->id . "\n";
    
} catch (\Exception $e) {
    echo "Error: " . $e->getMessage() . "\n";
}

```

## 4. Sending Email

```php
<?php

require 'vendor/autoload.php';

use CloudContactAI\CCAI\CCAI;
use CloudContactAI\CCAI\Email\Account;
use CloudContactAI\CCAI\Email\EmailCampaign;
use CloudContactAI\CCAI\Email\EmailOptions;

// Initialize the client
$ccai = new CCAI([
    'clientId' => 'YOUR-CLIENT-ID',
    'apiKey' => 'YOUR-API-KEY'
]);

// Send a single email
$response = $ccai->email->sendSingle(
    firstName: 'John',
    lastName: 'Doe',
    email: 'john@example.com',
    subject: 'Welcome to Our Service',
    message: '<p>Hello John,</p><p>Thank you for signing up!</p>',
    senderEmail: 'noreply@yourcompany.com',
    replyEmail: 'support@yourcompany.com',
    senderName: 'Your Company',
    title: 'Welcome Email'
);

echo "Email sent successfully!\n";

// Send email campaign to multiple recipients
$accounts = [
    new Account('John', 'Doe', 'john@example.com'),
    new Account('Jane', 'Smith', 'jane@example.com')
];

$campaign = new EmailCampaign(
    subject: 'Monthly Newsletter',
    title: 'July 2025 Newsletter',
    message: '<h1>Hello ${firstName}!</h1><p>Monthly updates...</p>',
    senderEmail: 'newsletter@yourcompany.com',
    replyEmail: 'support@yourcompany.com',
    senderName: 'Your Company Newsletter',
    accounts: $accounts
);

// Schedule for future delivery
$tomorrow = new DateTime('tomorrow 10:00:00');
$campaign->scheduledTimestamp = $tomorrow->format('c');
$campaign->scheduledTimezone = 'America/New_York';

// Add progress tracking
$options = new EmailOptions(
    timeout: 60,
    onProgress: function($status) {
        echo "Progress: $status\n";
    }
);

$response = $ccai->email->sendCampaign($campaign, $options);
echo "Campaign sent successfully!\n";
```

## 5. Webhooks

```
<?php

require 'vendor/autoload.php';

use CloudContactAI\CCAI\CCAI;
use CloudContactAI\CCAI\WebhookConfig;
use CloudContactAI\CCAI\WebhookEventType;
use CloudContactAI\CCAI\Webhook;

// Initialize the client
$ccai = new CCAI([
    'clientId' => 'YOUR-CLIENT-ID',
    'apiKey' => 'YOUR-API-KEY'
]);

// Register a webhook
$config = new WebhookConfig(
    url: 'https://your-domain.com/api/ccai-webhook',
    events: [WebhookEventType::MESSAGE_SENT, WebhookEventType::MESSAGE_RECEIVED],
    secret: 'your-webhook-secret'
);

$webhook = $ccai->webhook->register($config);
echo "Webhook registered with ID: {$webhook->id}\n";

// List all webhooks
$webhooks = $ccai->webhook->list();
echo "Found " . count($webhooks) . " webhooks\n";

// Create webhook handler
$handlers = [
    'onMessageSent' => function($event) {
        echo "Message sent: {$event->message} to {$event->to}\n";
    },
    'onMessageReceived' => function($event) {
        echo "Message received: {$event->message} from {$event->from}\n";
    }
];

$webhookHandler = Webhook::createHandler($handlers);

// Use in your web application
// $payload = json_decode(file_get_contents('php://input'), true);
// $result = $webhookHandler($payload);
```

### Example Files

Run the example files:

```
# Basic email sending
php send_email.php

# Advanced email campaigns with HTML templates and scheduling
php email_campaign_examples.php

# Webhook management and handling
php webhook_example.php
```

## 6. Contact Validator

Validate email addresses and phone numbers.

> Bulk endpoints accept up to 50 contacts per request and are processed server-side in chunks.

```php
<?php

require 'vendor/autoload.php';

use CloudContactAI\CCAI\CCAI;

$ccai = new CCAI([
    'clientId' => 'YOUR-CLIENT-ID',
    'apiKey' => 'YOUR-API-KEY'
]);

// Validate a single email
$emailResult = $ccai->contactValidator->validateEmail('user@example.com');
echo "Status: " . $emailResult['status'] . "\n"; // "valid" | "invalid" | "risky"

// Validate multiple emails (up to 50)
$bulkEmails = $ccai->contactValidator->validateEmails([
    'user@example.com',
    'bad@invalid.xyz'
]);
echo "Total: " . $bulkEmails['summary']['total'] . "\n"; // 2
echo "Valid: " . $bulkEmails['summary']['valid'] . "\n"; // 1

// Validate a single phone number
$phoneResult = $ccai->contactValidator->validatePhone('+15551234567', 'US');
echo "Status: " . $phoneResult['status'] . "\n"; // "valid" | "invalid" | "landline"

// Validate multiple phone numbers (up to 50)
$bulkPhones = $ccai->contactValidator->validatePhones([
    ['phone' => '+15551234567'],
    ['phone' => '+15559876543', 'countryCode' => 'US']
]);
echo "Landline: " . $bulkPhones['summary']['landline'] . "\n"; // 1
```

## 7. Brand Registration

Register and manage brands for TCR verification.

```php
<?php

require 'vendor/autoload.php';

use CloudContactAI\CCAI\CCAI;

$ccai = new CCAI([
    'clientId' => 'YOUR-CLIENT-ID',
    'apiKey' => 'YOUR-API-KEY'
]);

// Create a brand
$brand = $ccai->brands->create([
    'legalCompanyName' => 'Collect.org Inc.',
    'dba'              => 'Collect',
    'entityType'       => 'NON_PROFIT',
    'taxId'            => '123456789',
    'taxIdCountry'     => 'US',
    'country'          => 'US',
    'verticalType'     => 'NON_PROFIT',
    'websiteUrl'       => 'https://www.collect.org',
    'street'           => '123 Main Street',
    'city'             => 'San Francisco',
    'state'            => 'CA',
    'postalCode'       => '94105',
    'contactFirstName' => 'Jane',
    'contactLastName'  => 'Doe',
    'contactEmail'     => 'jane@collect.org',
    'contactPhone'     => '+14155551234',
]);
echo "Brand created with ID: " . $brand['id'] . "\n";

// Get a brand by ID
$fetched = $ccai->brands->get($brand['id']);
echo "Brand name: " . $fetched['legalCompanyName'] . "\n";

// List all brands
$brands = $ccai->brands->list();
echo "Total brands: " . count($brands) . "\n";

// Update a brand (partial update)
$ccai->brands->update($brand['id'], [
    'street' => '456 Oak Avenue',
    'city'   => 'Los Angeles',
]);

// Delete a brand
$ccai->brands->delete($brand['id']);
```

**Entity Types:** `PRIVATE_PROFIT`, `PUBLIC_PROFIT`, `NON_PROFIT`, `GOVERNMENT`, `SOLE_PROPRIETOR`

**Vertical Types:** `AUTOMOTIVE`, `AGRICULTURE`, `BANKING`, `COMMUNICATION`, `CONSTRUCTION`, `EDUCATION`, `ENERGY`, `ENTERTAINMENT`, `GOVERNMENT`, `HEALTHCARE`, `HOSPITALITY`, `INSURANCE`, `LEGAL`, `MANUFACTURING`, `NON_PROFIT`, `PROFESSIONAL`, `REAL_ESTATE`, `RETAIL`, `TECHNOLOGY`, `TRANSPORTATION`

## 8. Campaign Registration

Register and manage campaigns for TCR carrier vetting.

```php
<?php

require 'vendor/autoload.php';

use CloudContactAI\CCAI\CCAI;

$ccai = new CCAI([
    'clientId' => 'YOUR-CLIENT-ID',
    'apiKey' => 'YOUR-API-KEY'
]);

// Create a campaign
$campaign = $ccai->campaigns->create([
    'brandId'          => 1,
    'useCase'          => 'MIXED',
    'subUseCases'      => ['CUSTOMER_CARE', 'TWO_FACTOR_AUTHENTICATION', 'ACCOUNT_NOTIFICATION'],
    'description'      => 'Security codes and support messaging.',
    'messageFlow'      => 'Users opt-in via signup form at https://example.com/signup',
    'hasEmbeddedLinks' => true,
    'hasEmbeddedPhone' => false,
    'isAgeGated'       => false,
    'isDirectLending'  => false,
    'optInKeywords'    => ['START'],
    'optInMessage'     => 'Welcome! Reply STOP to cancel.',
    'optInProofUrl'    => 'https://example.com/opt-in-proof.png',
    'helpKeywords'     => ['HELP'],
    'helpMessage'      => 'For HELP email support@example.com.',
    'optOutKeywords'   => ['STOP'],
    'optOutMessage'    => 'STOP received. You are unsubscribed.',
    'sampleMessages'   => [
        'Your code is 554321. Reply STOP to cancel.',
        'Your ticket has been updated. Reply HELP for info.',
    ],
]);
echo "Campaign created with ID: " . $campaign['id'] . "\n";

// Get a campaign by ID
$fetched = $ccai->campaigns->get($campaign['id']);

// List all campaigns
$campaigns = $ccai->campaigns->list();
echo "Total campaigns: " . count($campaigns) . "\n";

// Update a campaign (partial update)
$ccai->campaigns->update($campaign['id'], [
    'description' => 'Updated description.',
]);

// Delete a campaign
$ccai->campaigns->delete($campaign['id']);
```

**Use Cases:** `TWO_FACTOR_AUTHENTICATION`, `ACCOUNT_NOTIFICATION`, `CUSTOMER_CARE`, `DELIVERY_NOTIFICATION`, `FRAUD_ALERT`, `HIGHER_EDUCATION`, `LOW_VOLUME_MIXED`, `MARKETING`, `MIXED`, `POLLING_VOTING`, `PUBLIC_SERVICE_ANNOUNCEMENT`, `SECURITY_ALERT`

> `MIXED` and `LOW_VOLUME_MIXED` campaigns require 2–3 `subUseCases`.

**Sub-Use Cases:** `TWO_FACTOR_AUTHENTICATION`, `ACCOUNT_NOTIFICATION`, `CUSTOMER_CARE`, `DELIVERY_NOTIFICATION`, `FRAUD_ALERT`, `MARKETING`, `POLLING_VOTING`

## Features

* Send SMS messages to single or multiple recipients
* Send MMS messages with images
* Send Email campaigns with HTML content
* Schedule emails for future delivery
* Webhook management (register, update, list, delete)
* Webhook event handling for web frameworks
* Variable substitution in messages (`${firstName}`, `${lastName}`)
* Progress tracking callbacks
* Type hints for better IDE integration
* Comprehensive error handling
* PSR-7 and PSR-18 compliant

## Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-php).
