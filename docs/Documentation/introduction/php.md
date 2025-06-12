---
title: PHP
excerpt: Send SMS with PHP
deprecated: false
hidden: false
metadata:
  robots: index
---
Learn how to send your first SMS using the CCAI PHP SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Paid Plan
* Create an API Key

## 1. Install

Get the CCAI PHP SDK

```node
composer require cloudcontactai/ccai-php
```

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

require 'vendor/autoload.php';

use CloudContactAI\CCAI\CCAI;
use CloudContactAI\CCAI\SMS\Account;
use CloudContactAI\CCAI\SMS\SMSOptions;

// Initialize the client
$ccai = new CCAI([
    'clientId' => 'YOUR-CLIENT-ID',
    'apiKey' => 'YOUR-API-KEY'
]);

// Method 1: All-in-one approach - Upload image and send MMS in one step
$imagePath = '/path/to/your/image.png';
$contentType = 'image/png';

// Create an account for the recipient
$account = new Account('John', 'Doe', '+15551234567');

// Optional: Create options with a progress callback
$options = new SMSOptions(
    timeout: 60,
    onProgress: function ($status) {
        echo "Status: $status\n";
    }
);

// Send MMS with image in one step
$response = $ccai->mms->sendWithImage(
    $imagePath,
    $contentType,
    [$account],
    'Hi ${firstName}, check out this image!',
    'MMS Campaign'
);

echo "MMS sent successfully! Campaign ID: " . $response->campaignId . "\n";

// Method 2: Step-by-step approach
// Step 1: Get a signed URL for uploading the image
$uploadResponse = $ccai->mms->getSignedUploadUrl(
    'image.png',
    'image/png'
);

$signedUrl = $uploadResponse['url'];
$fileKey = $uploadResponse['fileKey'];

// Step 2: Upload the image to the signed URL
$uploadSuccess = $ccai->mms->uploadImageToSignedUrl(
    $signedUrl,
    $imagePath,
    'image/png'
);

// Step 3: Send the MMS with the uploaded image
$response = $ccai->mms->send(
    $fileKey,
    [$account],
    'Hi ${firstName}, check out this image!',
    'MMS Campaign',
    $options
);

echo "MMS sent successfully! Campaign ID: " . $response->campaignId . "\n";
```

<br />

## 4. Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-php).