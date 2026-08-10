---
title: (02-01-24) Release Notes
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: 'CloudContactAI release 02/01/24: HubSpot workflow SMS actions, contacts migrated to Postgres, outbound SMS activity on HubSpot.'
  robots: index
next:
  description: ''
---
| Jira Ticket | Description                                                                                                  |
| :---------- | :----------------------------------------------------------------------------------------------------------- |
| CLOUD-1674  | Implemented workflows for Hubspot that let users embed SMS actions.                                          |
| CLOUD-1692  | Migrated the Contacts from MongoDB to Postgres, as MongoDB wasn't optimized for larger contact lists.        |
| CLOUD-1682  | Unknown phone\_types on Twilio are now appropriately marked as invalid phones.                               |
| CLOUD-1164  | Outbound SMS will now show up on the activity tabs on Hubspot.                                               |
| CLOUD-1677  | Fixed optimization issues with contact list aggregation.  Uploading and changing contact lists also updated. |
