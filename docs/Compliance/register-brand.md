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

**Base URL:** `https://compliance.cloudcontactai.com/api`

**Endpoint:**

```
POST /v1/brands
```

**JavaScript (SDK):**

```javascript
const brand = await ccai.brands.create({
  legalCompanyName: "Your Company LLC",
  entityType: "PRIVATE_PROFIT",
  taxId: "123456789",
  taxIdCountry: "US",
  country: "US",
  verticalType: "TECHNOLOGY",
  websiteUrl: "https://www.yourcompany.com",
  street: "123 Main St",
  city: "San Francisco",
  state: "CA",
  postalCode: "94105",
  contactFirstName: "Jane",
  contactLastName: "Smith",
  contactEmail: "compliance@yourcompany.com",
  contactPhone: "+14155551234"
});

console.log(`Brand ID: ${brand.id}`);
```

**cURL:**

```bash
curl -X POST https://compliance.cloudcontactai.com/api/v1/brands \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "legalCompanyName": "Your Company LLC",
    "entityType": "PRIVATE_PROFIT",
    "taxId": "123456789",
    "taxIdCountry": "US",
    "country": "US",
    "verticalType": "TECHNOLOGY",
    "websiteUrl": "https://www.yourcompany.com",
    "street": "123 Main St",
    "city": "San Francisco",
    "state": "CA",
    "postalCode": "94105",
    "contactFirstName": "Jane",
    "contactLastName": "Smith",
    "contactEmail": "compliance@yourcompany.com",
    "contactPhone": "+14155551234"
  }'
```

## Request Parameters

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `legalCompanyName` | string | Yes | The registered legal name of your business |
| `entityType` | string | Yes | Business entity type (see options below) |
| `taxId` | string | Yes | Your business tax ID (9 digits for US/CA) |
| `taxIdCountry` | string | Yes | Country where the tax ID is registered (US, CA, GB, AU) |
| `country` | string | Yes | Country of business operations |
| `verticalType` | string | Yes | Business vertical (see options below) |
| `websiteUrl` | string | Yes | Your company website URL (must start with http:// or https://) |
| `street` | string | Yes | Registered business street address |
| `city` | string | Yes | City |
| `state` | string | Yes | State or province |
| `postalCode` | string | Yes | Postal/ZIP code |
| `contactFirstName` | string | Yes | Compliance contact first name |
| `contactLastName` | string | Yes | Compliance contact last name |
| `contactEmail` | string | Yes | Compliance contact email |
| `contactPhone` | string | Yes | Compliance contact phone number |
| `dba` | string | No | "Doing Business As" name if different from legal name |
| `stockSymbol` | string | Conditional | Required for PUBLIC_PROFIT entities |
| `stockExchange` | string | Conditional | Required for PUBLIC_PROFIT entities |

### Supported Entity Types

- `PRIVATE_PROFIT`
- `PUBLIC_PROFIT`
- `NON_PROFIT`
- `GOVERNMENT`
- `SOLE_PROPRIETOR`

### Supported Vertical Types

- `AUTOMOTIVE`
- `AGRICULTURE`
- `BANKING`
- `COMMUNICATION`
- `CONSTRUCTION`
- `EDUCATION`
- `ENERGY`
- `ENTERTAINMENT`
- `GOVERNMENT`
- `HEALTHCARE`
- `HOSPITALITY`
- `INSURANCE`
- `LEGAL`
- `MANUFACTURING`
- `NON_PROFIT`
- `PROFESSIONAL`
- `REAL_ESTATE`
- `RETAIL`
- `TECHNOLOGY`
- `TRANSPORTATION`

### Supported Stock Exchanges (for PUBLIC_PROFIT)

- `NASDAQ`
- `NYSE`
- `AMEX`
- `TSX`
- `LON`
- `JPX`
- `HKEX`
- `OTHER`

## Response

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
  "updatedAt": "2026-08-10T15:00:00Z"
}
```

## Other Brand Endpoints

| Operation | Method | Endpoint |
|-----------|--------|----------|
| List brands | GET | `/v1/brands` |
| Get brand | GET | `/v1/brands/{id}` |
| Update brand | PATCH | `/v1/brands/{id}` |
| Delete brand | DELETE | `/v1/brands/{id}` |

## Validation Rules

- Tax ID must be exactly 9 digits for US and CA
- Website URL must start with `http://` or `https://`
- Contact email must be a valid email format
- PUBLIC_PROFIT entities require `stockSymbol` and `stockExchange`

## What Happens Next

After submitting your brand registration:

1. Your submission is created and stored
2. Review typically takes 1 to 7 business days
3. Once approved, you can proceed to [Register a Campaign](https://developer.cloudcontactai.com/docs/register-campaign)

Use the [Check Registration Status](https://developer.cloudcontactai.com/docs/check-registration-status) endpoint to monitor your brand approval.
