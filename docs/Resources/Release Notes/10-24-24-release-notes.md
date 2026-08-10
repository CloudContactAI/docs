---
title: (10-24-24) Release Notes
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: 'CloudContactAI release 10/24/24: ChatGPT-powered configurable chatbot, EKS upgrade, voice campaign module removed.'
  robots: index
next:
  description: ''
---
| Jira Ticket | Description                                                                                                                         |
| :---------- | :---------------------------------------------------------------------------------------------------------------------------------- |
| CLOUD-1857  | Updated EKS to run on an updated version over the depreciated version we used.                                                      |
| CLOUD-1899  | Email messages are now tagged with client and account IDs so we can make straight queries.                                          |
| CLOUD-1898  | Hid voice campaign module and options from the UI and remove the microservices from K8S.                                            |
| CLOUD-1901  | Fixed an issue where sent email campaigns weren't appearing on the stats dashboard or the sent tab.                                 |
| CLOUD-1908  | Added a configurable chatbot powered by ChatGPT that uses the current campaign as context.                                          |
| CLOUD-1883  | Fixed an issue where some email campaigns bounced, yet they had dates for when the recipient clicked on a link or opened the email. |
| CLOUD-1887  | Fixed an error with redirect phone numbers and Telnyx and Twilio.                                                                   |
