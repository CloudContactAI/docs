---
title: (02-04-25) Release Notes
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
| Jira Ticket | Description                                                                                                                                                                                    |
| :---------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CLOUD-1982  | Fixed an issue where changing a client name would break an AWS Simple Email Service configuration.                                                                                             |
| CLOUD-1976  | Setting a from-email address will establish it as the default reply-to address.                                                                                                                |
| CLOUD-1975  | When sending an email campaign, contact lists couldn't be organized by list size.                                                                                                              |
| CLOUD-1895  | Fixed an issue where sending a campaign with multiple from-addresses would cause the fields "From Email," "From Name," and "Reply-To Email" to disappear.                                      |
| CLOUD-1967  | Adjusted the wording seen in the email builder.                                                                                                                                                |
| CLOUD-1973  | Emails that bounce will now be marked as bounced under the contact details.                                                                                                                    |
| CLOUD-1977  | Fixed issue where email flows would not save properly.                                                                                                                                         |
| CLOUD-1980  | Fixed issue where automated emails weren't appearing on the email campaign list.                                                                                                               |
| CLOUD-1988  | Added support for multiple CCAI accounts to be mapped to a single Enterprise-tier HubSpot account.                                                                                             |
| CLOUD-1994  | Fixed issue where searching for a contact with a term that didn't exist in contact records while making an email campaign would result in the app forgetting any previously selected contacts. |