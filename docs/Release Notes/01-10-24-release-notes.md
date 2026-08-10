---
title: (01-10-24) Release Notes
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: 'CloudContactAI release 01/10/24: HubSpot workflow support, outbound SMS on HubSpot activity page, duplicate campaign safeguards.'
  robots: index
next:
  description: ''
---
| Jira Ticket | Description                                                                                                                             |
| :---------- | :-------------------------------------------------------------------------------------------------------------------------------------- |
| CLOUD-1164  | Outbound SMS messages will now be visible in the activity Overview page on Hubspot.                                                     |
| CLOUD-1674  | Added ability to create workflows and use them from the Hubspot attachment.                                                             |
| CLOUD-1662  | Now can add contacts from one list onto another list.                                                                                   |
| CLOUD-1671  | Fixed case-sensitivity issue when adding clients onto an account.                                                                       |
| CLOUD-1686  | Email campaigns were for some reason not recording activity on the chart during Mondays, Wednesdays, and Fridays.                       |
| CLOUD-1679  | Added safeguards that ensures that we do not send the same bulk campaign message to the same contact within a specified period of time. |
