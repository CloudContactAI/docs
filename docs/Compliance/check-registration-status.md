---
title: Check Registration Status
excerpt: >-
  Monitor the approval status of your A2P 10DLC brand and campaign registrations with CloudContactAI.
deprecated: false
hidden: false
metadata:
  title: Check A2P 10DLC Registration Status | CloudContactAI Compliance API
  description: Poll and monitor the approval status of your brand and campaign registrations for A2P 10DLC compliance using the CloudContactAI SDK.
  keywords:
    - A2P 10DLC
    - registration status
    - brand approval
    - campaign approval
    - SMS compliance
    - CloudContactAI
  robots: index
---

> Monitor your brand and campaign registration status to know when your A2P 10DLC submissions are approved.

## Overview

After submitting brand and campaign registrations, you can programmatically check their approval status. This is useful for automating your onboarding flow or building dashboards that track compliance readiness.

## Check Brand Status

Retrieve the current status of a brand registration.

**Endpoint:**

```
GET https://core.cloudcontactai.com/api/compliance/brands/{brandId}/status
```

**JavaScript (SDK):**

```javascript
const brandStatus = await ccai.compliance.getBrandStatus(brand.brandId);
console.log(`Brand Status: ${brandStatus.status}`); // PENDING, APPROVED, REJECTED
```

**cURL:**

```bash
curl -X GET https://core.cloudcontactai.com/api/compliance/brands/BRAND_abc123/status \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

**Response:**

```json
{
  "brandId": "BRAND_abc123",
  "status": "APPROVED",
  "updatedAt": "2026-08-12T10:00:00Z",
  "reason": null
}
```

## Check Campaign Status

Retrieve the current status of a campaign registration.

**Endpoint:**

```
GET https://core.cloudcontactai.com/api/compliance/campaigns/{campaignId}/status
```

**JavaScript (SDK):**

```javascript
const campaignStatus = await ccai.compliance.getCampaignStatus(campaign.campaignId);
console.log(`Campaign Status: ${campaignStatus.status}`); // PENDING, APPROVED, REJECTED
```

**cURL:**

```bash
curl -X GET https://core.cloudcontactai.com/api/compliance/campaigns/CAMP_xyz789/status \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

**Response:**

```json
{
  "campaignId": "CAMP_xyz789",
  "status": "PENDING",
  "updatedAt": "2026-08-10T15:30:00Z",
  "reason": null
}
```

## Status Values

| Status | Description |
|--------|-------------|
| `PENDING` | Registration submitted and awaiting carrier review |
| `APPROVED` | Registration approved, ready for use |
| `REJECTED` | Registration rejected (check the `reason` field for details) |

## Polling for Approval

If you need to wait for approval before proceeding, you can poll the status endpoint at regular intervals.

**JavaScript (SDK):**

```javascript
async function waitForApproval(brandId, intervalMs = 30000) {
  let status = 'PENDING';
  while (status === 'PENDING') {
    const result = await ccai.compliance.getBrandStatus(brandId);
    status = result.status;
    if (status === 'PENDING') {
      console.log('Still pending, checking again in 30s...');
      await new Promise(resolve => setTimeout(resolve, intervalMs));
    }
  }
  return status;
}

// Usage
const finalStatus = await waitForApproval(brand.brandId);
if (finalStatus === 'APPROVED') {
  console.log('Brand approved! Proceeding to campaign registration...');
} else {
  console.log('Brand rejected. Check the reason and resubmit.');
}
```

**Python:**

```python
import time
import requests

def wait_for_brand_approval(brand_id, api_key, interval=30):
    status = 'PENDING'
    while status == 'PENDING':
        response = requests.get(
            f'https://core.cloudcontactai.com/api/compliance/brands/{brand_id}/status',
            headers={
                'Authorization': f'Bearer {api_key}',
                'Content-Type': 'application/json'
            }
        )
        result = response.json()
        status = result['status']
        if status == 'PENDING':
            print('Still pending, checking again in 30s...')
            time.sleep(interval)
    return status

# Usage
final_status = wait_for_brand_approval('BRAND_abc123', 'YOUR_API_KEY')
if final_status == 'APPROVED':
    print('Brand approved! Proceeding to campaign registration...')
else:
    print('Brand rejected. Check the reason and resubmit.')
```

## Handling Rejections

If a registration is rejected, the response includes a `reason` field explaining why.

```json
{
  "brandId": "BRAND_abc123",
  "status": "REJECTED",
  "updatedAt": "2026-08-12T10:00:00Z",
  "reason": "Tax ID does not match the provided legal name"
}
```

**Common rejection reasons:**

- Tax ID does not match the provided legal name
- Website domain does not match registered business
- Insufficient business information provided
- Sample messages do not include required opt-out language
- Message flow description lacks clear opt-in consent mechanism

After addressing the rejection reason, you can submit a new registration.

## Recommended Polling Intervals

- **Brand registration:** Poll every 30 to 60 seconds during testing, every 1 to 4 hours in production
- **Campaign registration:** Poll every 30 to 60 seconds during testing, every 1 to 4 hours in production

Carrier review timelines vary. Brand reviews typically take 1 to 7 business days, and campaign reviews take 1 to 5 business days.
