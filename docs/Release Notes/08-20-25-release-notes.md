---
title: (08-20-25) Release Notes
deprecated: false
hidden: false
metadata:
  robots: index
---
| Jira Ticket | Description                                                                                                                                                                                             |
| :---------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CLOUD-2259  | Added the client ID and campaign name to the billing tab information.                                                                                                                                   |
| CLOUD-2300  | Added Force Credit Card functionality. Upon loggin, a user will be locked out of all functionality until they put down a card. This is an administrative feature meant to enforce payment method entry. |
| CLOUD-2320  | Fixed an issue where using the API to send a default campaign would result in an error that trial accounts wouldn't see.                                                                                |
| CLOUD-2310  | Fixed an issue where Last Reassign Lookup date was erroneously displayed in the Last Reassign date category.                                                                                            |
| CLOUD-2331  | Remove the Account ID requirement on API calls that do not forcibly require it.                                                                                                                         |
| CLOUD-2341  | Fixed minor proportion issues in the email builder.                                                                                                                                                     |
| CLOUD-2342  | Email editor quality-of-life changes.                                                                                                                                                                   |
| CLOUD-2327  | Fixed an issue where cent values weren't respected as they were on Stripe.                                                                                                                              |
| CLOUD-2321  | Account limit values are cached to make changing and updating them from admin easier.                                                                                                                   |
| CLOUD-2315  | Added auto-responses to the web socket.                                                                                                                                                                 |
| CLOUD-2347  | Prioritized a client during ACH verification for faster completion.                                                                                                                                     |
| CLOUD-2333  | Added option to manually change account password.                                                                                                                                                       |
| CLOUD-2343  | Added option to name email templates. The template dropdown in the email builder now uses the template name instead of the subject.                                                                     |
| CLOUD-2355  | AI prompts in the settings tab are now by account instead of by client.                                                                                                                                 |
| CLOUD-2357  | Fixed an issue with duplicate billing entries on Stripe.                                                                                                                                                |
| CLOUD-2211  | Fixed an issue with the OpenAI Intents limit not properly limiting the user.                                                                                                                            |
| CLOUD-2209  | Newly paid accounts will now default to the Auto Charge functionality.                                                                                                                                  |
| CLOUD-2319  | Added an AI to clean the inbox of contacts labeled as "do not contact."                                                                                                                                 |
| CLOUD-2348  | Fixed billing taking into consideration toll-free phone numbers.                                                                                                                                        |
| CLOUD-2350  | Added new last\_action\_date category for SMS campaigns.                                                                                                                                                |
| CLOUD-2091  | Email designs are now saved outside of MongoDB.                                                                                                                                                         |
| CLOUD-2318  | SMS segments are now displayed on the SMS dashboard.                                                                                                                                                    |
| CLOUD-2360  | Added option to change an account password from the Admin view.                                                                                                                                         |