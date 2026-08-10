---
title: Check Registration Status
excerpt: >-
  Monitor the status of your A2P 10DLC brand and campaign registrations with CloudContactAI.
deprecated: false
hidden: false
metadata:
  title: Check A2P 10DLC Registration Status | CloudContactAI Compliance API
  description: Monitor the status of your brand and campaign registrations for A2P 10DLC compliance using the CloudContactAI SDK.
  keywords:
    - A2P 10DLC
    - registration status
    - brand approval
    - campaign approval
    - SMS compliance
    - CloudContactAI
  robots: index
---

> Monitor your brand and campaign registration status to track your A2P 10DLC submissions.

## Overview

After submitting brand and campaign registrations, you can programmatically retrieve their details and check their status. This is useful for automating your onboarding flow or building dashboards that track compliance readiness.

**Base URL:** `https://compliance.cloudcontactai.com/api`

## Check Brand Status

Retrieve the details of a specific brand registration.

**Endpoint:**

```
GET /v1/brands/{id}
```

**JavaScript (SDK):**

```javascript
const brand = await ccai.brands.get(123);
console.log(`Brand: ${brand.legalCompanyName}`);
console.log(`Created: ${brand.createdAt}`);
console.log(`Updated: ${brand.updatedAt}`);
```

**cURL:**

```bash
curl -X GET https://compliance.cloudcontactai.com/api/v1/brands/123 \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

**Response:**

```json
{
  "id": 123,
  "accountId": 456,
  "legalCompanyName": "Your Company LLC",
  "entityType": "PRIVATE_PROFIT",
  "taxId": "123456789",
  "taxIdCountry": "US",
  "country": "US",
  "verticalType": "TECHNOLOGY",
  "websiteUrl": "https://www.yourcompany.com",
  "websiteMatchScore": null,
  "street": "123 Main St",
  "city": "San Francisco",
  "state": "CA",
  "postalCode": "94105",
  "contactFirstName": "Jane",
  "contactLastName": "Smith",
  "contactEmail": "compliance@yourcompany.com",
  "contactPhone": "+14155551234",
  "createdAt": "2026-08-10T15:00:00Z",
  "updatedAt": "2026-08-12T10:00:00Z"
}
```

## List All Brands

Retrieve all brand registrations for your account.

**Endpoint:**

```
GET /v1/brands
```

**JavaScript (SDK):**

```javascript
const brands = await ccai.brands.list();
brands.forEach(brand => {
  console.log(`${brand.id}: ${brand.legalCompanyName}`);
});
```

**cURL:**

```bash
curl -X GET https://compliance.cloudcontactai.com/api/v1/brands \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Check Campaign Status

Retrieve the details of a specific campaign registration.

**Endpoint:**

```
GET /v1/campaigns/{id}
```

**JavaScript (SDK):**

```javascript
const campaign = await ccai.campaigns.get(789);
console.log(`Campaign: ${campaign.useCase}`);
console.log(`Brand ID: ${campaign.brandId}`);
console.log(`Monthly Fee: $${campaign.monthlyFee}`);
console.log(`Created: ${campaign.createdAt}`);
```

**cURL:**

```bash
curl -X GET https://compliance.cloudcontactai.com/api/v1/campaigns/789 \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

**Response:**

```json
{
  "id": 789,
  "accountId": 456,
  "brandId": 123,
  "useCase": "MARKETING",
  "description": "Promotional messages for opted-in customers",
  "messageFlow": "Customers opt-in via web form and receive promotional SMS",
  "hasEmbeddedLinks": true,
  "hasEmbeddedPhone": false,
  "isAgeGated": false,
  "isDirectLending": false,
  "optInKeywords": ["START", "YES"],
  "optInMessage": "You are now subscribed. Reply STOP to unsubscribe.",
  "optInProofUrl": "https://www.yourcompany.com/sms-opt-in",
  "helpKeywords": ["HELP", "INFO"],
  "helpMessage": "Reply HELP for assistance. Contact support@yourcompany.com.",
  "optOutKeywords": ["STOP", "CANCEL", "UNSUBSCRIBE"],
  "optOutMessage": "You have been unsubscribed. Reply START to re-subscribe.",
  "sampleMessages": [
    "Hi Jane, check out our latest deals at https://example.com. Reply STOP to opt out.",
    "Your order #12345 has shipped! Reply HELP for help."
  ],
  "monthlyFee": 10.00,
  "createdAt": "2026-08-10T15:30:00Z",
  "updatedAt": "2026-08-10T15:30:00Z"
}
```

## List All Campaigns

Retrieve all campaign registrations for your account.

**Endpoint:**

```
GET /v1/campaigns
```

**JavaScript (SDK):**

```javascript
const campaigns = await ccai.campaigns.list();
campaigns.forEach(campaign => {
  console.log(`${campaign.id}: ${campaign.useCase} (Brand: ${campaign.brandId})`);
});
```

**cURL:**

```bash
curl -X GET https://compliance.cloudcontactai.com/api/v1/campaigns \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

---

## Polling for Status Changes

If you need to monitor registrations for status changes, you can poll the endpoints at regular intervals.

**JavaScript:**

```javascript
async function pollBrandStatus(brandId, intervalMs = 30000) {
  let previousUpdatedAt = null;

  while (true) {
    const brand = await ccai.brands.get(brandId);

    if (brand.updatedAt !== previousUpdatedAt) {
      console.log(`Brand ${brand.id} updated at: ${brand.updatedAt}`);
      previousUpdatedAt = brand.updatedAt;
    }

    console.log('Checking again in 30s...');
    await new Promise(resolve => setTimeout(resolve, intervalMs));
  }
}
```

**Python:**

```python
import time
import requests

def poll_brand(brand_id, api_key, interval=30):
    previous_updated = None

    while True:
        response = requests.get(
            f'https://compliance.cloudcontactai.com/api/v1/brands/{brand_id}',
            headers={
                'Authorization': f'Bearer {api_key}',
                'Content-Type': 'application/json'
            }
        )
        brand = response.json()

        if brand['updatedAt'] != previous_updated:
            print(f"Brand {brand['id']} updated at: {brand['updatedAt']}")
            previous_updated = brand['updatedAt']

        print('Checking again in 30s...')
        time.sleep(interval)
```

## Recommended Polling Intervals

- **During testing:** Every 30 to 60 seconds
- **In production:** Every 1 to 4 hours

Carrier review timelines vary. Brand reviews typically take 1 to 7 business days, and campaign reviews take 1 to 5 business days.
