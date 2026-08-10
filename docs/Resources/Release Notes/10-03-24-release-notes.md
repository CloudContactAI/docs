---
title: (10-03-24) Release Notes
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: 'CloudContactAI release 10/03/24: multi-domain email sending, email builder field dropdown, HubSpot chatbot integration.'
  robots: index
next:
  description: ''
---
| Jira Ticket | Description                                                                                                                                                                |
| :---------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CLOUD-1847  | Email campaigns going out to large lists can now be split and sent from multiple different domains.                                                                        |
| CLOUD-1861  | Email builder now has a dropdown for adding fields to emails; i.e., inserting a first name and last name.                                                                  |
| CLOUD-1865  | Fixed an issue where opening the email template builder would redirect the user back to the email campaign screen.                                                         |
| CLOUD-1859  | Added a chatbot to the HubSpot integration.                                                                                                                                |
| CLOUD-1873  | Made corrections to error rate calculations.                                                                                                                               |
| CLOUD-1880  | Campaign stats just update numbers with each subsequent launch rather than needing to recalculate everything.                                                              |
| CLOUD-1879  | Fixed an issue where if HubSpot communications fail to finish their processing, an exception would be thrown on the process on core-jobs, which made this fail every time. |
| CLOUD-1878  | Direct campaigns now should always send messages through the default campaign.                                                                                             |
| CLOUD-1875  | Adjusted spacing around the 'next' button on the first page of the email builder.                                                                                          |
| CLOUD-1872  | Changed SMS Stats calculations to use a lighter view which hits some of the biggest tables on the system.  This should ease processing for the databases.                  |
| CLOUD-1870  | Added client ID and account ID to the individual campaigns for easier filtering.                                                                                           |
