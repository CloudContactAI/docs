---
title: One-Time Password SMS Verification
deprecated: false
hidden: true
metadata:
  robots: index
---
Sending one-time passwords via SMS is a great way to keep your customers' credentials safe. Unlike static passwords, OTPs expire after one use or a short time window - typically 30 to 60 seconds - providing the least amount of surface area for potential attackers to steal client credentials with. It's a convenient system for both parties since it doesn't require a designated app and it can all be done through a single API integration.

### OTP Compared to Other Methods

| **Method**             | **Pros**                                              | **Cons**                              |
| ---------------------- | ----------------------------------------------------- | ------------------------------------- |
| **SMS OTP (CloudOTP)** | No app install, universal device support, familiar UX | Requires phone number                 |
| **Authenticator Apps** | No network dependency, works offline                  | Requires app install, user friction   |
| **Email OTP**          | Works without phone number                            | Slower delivery, often missed in spam |
| **Hardware Tokens**    | Highest security                                      | Expensive, easy to lose               |

<br />

### Implementation via the API

For more on how to use the CCAI API, check out the corresponding part of the documentation [here](https://developer.cloudcontactai.com/docs/quickstart-with-api?_gl=1*1e4l4lb*_gcl_au*MTc4NjQ4MDM2Ni4xNzgzNTIzMDY3LjgwNjMwNTIyNi4xNzg1MjYzNDI1LjE3ODUyNjM1NDEuMTEzNDEyNTA4OC4xNzg1MjYzNDI1LjE3ODUyNjM1NDE.*_ga*Nzc1NjAxMjMuMTY3NjQyNjkwMA..*_ga_XXYEEKXMFX*czE3ODU1MjA3MzckbzI5MCRnMSR0MTc4NTUyMDc1NSRqNDIkbDAkaDAkZEZLLUl4UEVpdmRFRXpmMzhPbkx2WWliZU83Wi1tajgyNXc.).

```cplusplus Sending OTP
# Request an OTP code be sent to a phone number
curl -X POST https://api.cloudcontactai.com/otp/send \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "phone_number": "+14155551234",
    "expiration_seconds": 60
  }'

```
```cplusplus Response
{
  "status": "sent",
  "otp_id": "otp_8f3k2j1",
  "expires_at": "2026-07-21T14:31:40Z"
}
```
```cplusplus Verify OTP
# Validate the code entered by the user
curl -X POST https://api.cloudcontactai.com/otp/verify \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "otp_id": "otp_8f3k2j1",
    "code": "847291"
  }'

```
