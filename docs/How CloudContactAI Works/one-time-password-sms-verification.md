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

<br />
