---
title: (06-25-24) Release Notes
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
| Jira Ticket | Description                                                                                                                                                                                  |
| :---------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CLOUD-1802  | Activities on CCAI will now appear on HubSpot if the accounts are linked.                                                                                                                    |
| CLOUD-1702  | Made adjustments to the SMS dashboard charts to better display high-volume campaign outputs.                                                                                                 |
| CLOUD-1668  | Fixed some inconsistencies with the email dashboard and the actual email output.                                                                                                             |
| CLOUD-1796  | Accounts that sign in using Google on a Cognito window are now easier to remove.                                                                                                             |
| CLOUD-1810  | Incoming message webhooks work for Telnyx and Twilio. Correctly called with an object that has the message non-private information.                                                          |
| CLOUD-1809  | The scope of the sent SMS and email tabs will now default to the past 30 days.                                                                                                               |
| CLOUD-1808  | The status category of the SMS sent tab will default to all types.                                                                                                                           |
| CLOUD-1813  | Fixed an issue where if a contact list was uploaded with an email category that had no entries for any contact, drilling into any contact would show no contact information in any category. |
| CLOUD-1772  | Fixed an issue where putting blank spaces before any of the names in first name, last name, and email would cause validation errors in each of those categories.                             |
