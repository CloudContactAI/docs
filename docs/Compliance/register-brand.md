---
title: Register Brand
excerpt: >-
  Register your brand for A2P 10DLC compliance with CloudContactAI to enable trusted business messaging.
deprecated: false
hidden: false
metadata:
  title: A2P 10DLC Brand Registration | CloudContactAI Compliance API
  description: Register your brand for A2P 10DLC compliance using the CloudContactAI SDK. Submit your business details programmatically to enable trusted SMS messaging.
  keywords:
    - A2P 10DLC
    - brand registration
    - SMS compliance
    - CloudContactAI
    - business messaging
  robots: index
---

> Register your brand for A2P 10DLC compliance to send trusted business SMS messages.

## Overview

A2P 10DLC (Application-to-Person 10-Digit Long Code) is a system that allows businesses to send SMS messages using standard 10-digit phone numbers with carrier-approved throughput. Brand registration is the first step in the A2P 10DLC compliance process.

Registering your brand establishes your business identity with carriers, which improves message deliverability and reduces the risk of filtering.

## Prerequisites

- A CloudContactAI account with API access
- Your business legal name, tax ID (EIN), and registered address
- A company website and compliance contact information

## Register Your Brand

Use the CloudContactAI SDK to submit your brand registration programmatically.

**Endpoint:**

```
POST https://core.cloudcontactai.com/api/compliance/brands
```

**JavaScript (SDK):**

```javascript
const brand = await ccai.compliance.registerBrand({
  legalName: "Your Company LLC",
  taxId: "12-3456789",
  taxIdCountry: "US",
  website: "https://www.yourcompany.com",
  vertical: "TECHNOLOGY",
  entityType: "PRIVATE_PROFIT",
  address: {
    street: "123 Main St",
    city: "San Francisco",
    state: "CA",
    postalCode: "94105",
    country: "US"
  },
  contactEmail: "compliance@yourcompany.com",
  contactPhone: "+14155551234"
});

console.log(`Brand ID: ${brand.brandId}`);
console.log(`Brand Status: ${brand.status}`);
```

**cURL:**

```bash
curl -X POST https://core.cloudcontactai.com/api/compliance/brands \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "legalName": "Your Company LLC",
    "taxId": "12-3456789",
    "taxIdCountry": "US",
    "website": "https://www.yourcompany.com",
    "vertical": "TECHNOLOGY",
    "entityType": "PRIVATE_PROFIT",
    "address": {
      "street": "123 Main St",
      "city": "San Francisco",
      "state": "CA",
      "postalCode": "94105",
      "country": "US"
    },
    "contactEmail": "compliance@yourcompany.com",
    "contactPhone": "+14155551234"
  }'
```

## Request Parameters

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `legalName` | string | Yes | The registered legal name of your business |
| `taxId` | string | Yes | Your business tax ID (EIN for US companies) |
| `taxIdCountry` | string | Yes | Country where the tax ID is registered (ISO 3166-1 alpha-2) |
| `website` | string | Yes | Your company website URL |
| `vertical` | string | Yes | Business vertical (see options below) |
| `entityType` | string | Yes | Business entity type (see options below) |
| `address` | object | Yes | Registered business address |
| `contactEmail` | string | Yes | Compliance contact email |
| `contactPhone` | string | Yes | Compliance contact phone number in E.164 format |

### Supported Verticals

- `TECHNOLOGY`
- `HEALTHCARE`
- `FINANCE`
- `RETAIL`
- `REAL_ESTATE`
- `EDUCATION`
- `INSURANCE`
- `ENTERTAINMENT`
- `TRANSPORTATION`
- `NON_PROFIT`
- `GOVERNMENT`
- `OTHER`

### Supported Entity Types

- `PRIVATE_PROFIT`
- `PUBLIC_PROFIT`
- `NON_PROFIT`
- `GOVERNMENT`
- `SOLE_PROPRIETOR`

## Response

```json
{
  "brandId": "BRAND_abc123",
  "legalName": "Your Company LLC",
  "status": "PENDING",
  "createdAt": "2026-08-10T15:00:00Z"
}
```

## What Happens Next

After submitting your brand registration:

1. Your submission enters a **PENDING** state for carrier review
2. Review typically takes 1 to 7 business days
3. You will receive a status update (APPROVED or REJECTED)
4. Once approved, you can proceed to [Register a Campaign](https://developer.cloudcontactai.com/docs/register-campaign)

Use the [Check Registration Status](https://developer.cloudcontactai.com/docs/check-registration-status) endpoint to monitor your brand approval.
