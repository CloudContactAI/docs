---
title: (09-28-23) Release Notes
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
| Jira Ticket | Description                                                                                                     |
| :---------- | :-------------------------------------------------------------------------------------------------------------- |
| CLOUD-1488  | Fixed an account's client's issue with increased loading times when searching through their contacts.           |
| CLOUD-1494  | Improved loading times when using the search function for larger contact lists.                                 |
| CLOUD-1537  | Removed the 'unsubscribed contacts' list from the contacts tab due to performance issues.                       |
| CLOUD-1522  | Fixed an account's contact list loading times.                                                                  |
| CLOUD-1504  | Updated the CampaignSender microservice to manage different SMS senders according to the Account configuration. |
| CLOUD-1502  | Implemented the Telnyx Webhook handler into SMSTracker microservice.                                            |
| CLOUD-1501  | Created a new Telnyx SMS/MMS Sender implementation.                                                             |
| CLOUD-1503  | Added the ability to set up Telnyx configuration by Account.                                                    |
| CLOUD-1505  | Added the ability to set up Telnyx configurations for the Trial/OTP senders.                                    |
| CLOUD-1507  | Implemented an incoming SMS Webhook Handler for Telnyx.                                                         |
| CLOUD-1508  | Implemented the option for Phone Number purchase in Telnyx.                                                     |
