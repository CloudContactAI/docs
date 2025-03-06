---
title: (03-23-23) Release Notes
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
[block:parameters]
{
  "data": {
    "0-0": "CLOUD-1201",
    "1-0": "CLOUD-1102",
    "2-0": "CLOUD-1022",
    "3-0": "CLOUD-1238",
    "4-0": "CLOUD-1239",
    "5-0": "CLOUD-1032",
    "6-0": "CLOUD-1220",
    "7-0": "CLOUD-1212",
    "8-0": "CLOUD-1221",
    "9-0": "CLOUD-1224",
    "10-0": "CLOUD-1249",
    "11-0": "CLOUD-1223",
    "12-0": "CLOUD-1226",
    "13-0": "CLOUD-1232",
    "14-0": "CLOUD-1222",
    "15-0": "CLOUD-1218",
    "1-1": "Fixed issue when importing a CSV file of contacts, if there is a column with empty variables that aren't the first name, last name, or phone number, the upload won't fail.",
    "0-1": "The auto response checkbox on a phone number in the settings tab is now more properly aligned with the other lines.",
    "2-1": "Added block inbound calls/text messages checkbox on contact settings.",
    "3-1": "Fixed issue where putting in an invalid time when scheduling an SMS or email campaign would completely prevent launching the campaign regardless of whether the date had been changed to a valid value.",
    "4-1": "Duplicate of CLOUD-1238.",
    "5-1": "Fixed issue where an error would occur when launching a campaign and using the \"+ add contacts\" option.",
    "6-1": "Added an automated email that alerts the user in the case of a failed CSV upload.",
    "7-1": "Increased character limit of the email title.",
    "8-1": "Admin is now internally alerted to CSV upload failures.",
    "9-1": "Fixed an issue with searching contacts when making a new contact list from existing contacts.",
    "10-1": "Changed URL shortener to where only trusted accounts have access to that feature.",
    "11-1": "Added an alert when making an SMS campaign.  If the user applies a custom variable not previously defined in any of the contacts receiving the campaign.",
    "12-1": "Changed the wording when deleting a contact.",
    "13-1": "Fixed an issue with the First Campaign upon signup.",
    "14-1": "Fixed an issue where Canadian phone numbers couldn't be reached.",
    "15-1": "With the new limitations on non-company emails for signup, the signup page will now highlight errors appropriately.",
    "h-0": "Jira Ticket",
    "h-1": "Description"
  },
  "cols": 2,
  "rows": 16
}
[/block]