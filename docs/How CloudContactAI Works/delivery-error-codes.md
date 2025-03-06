---
title: Delivery Error Codes
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
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c147217-Screenshot_2022-10-14_092031.png",
        "Screenshot 2022-10-14 092031.png",
        772,
        323,
        "#000000"
      ]
    }
  ]
}
[/block]
Whenever users look at a campaign that failed to go out, and the associated error code that comes tied with it when the cursor hovers over the error icon.  Here are what those codes mean.
[block:api-header]
{
  "title": "Internal Errors"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "CCAI-ERR-00",
    "0-1": "Phone validation error",
    "1-0": "CCAI-ERR-01",
    "1-1": "Landline",
    "2-0": "CCAI-ERR-02",
    "2-1": "Carrier Stated Landline",
    "3-0": "CCAI-ERR-03",
    "4-0": "CCAI-ERR-10",
    "5-0": "CCAI-ERR-1",
    "6-0": "2001",
    "7-0": "1000",
    "8-0": "1001",
    "3-1": "Invalid Phone Number",
    "4-1": "SMS Quota Exceeded",
    "5-1": "Unexpected",
    "6-1": "User asked to not text them (OptOut error)",
    "7-1": "This account has exceeded trial SMS limit",
    "8-1": "This client has exceeded monthly SMS limit"
  },
  "cols": 2,
  "rows": 9
}
[/block]

[block:api-header]
{
  "title": "Common Twilio Errors"
}
[/block]
There are many more than documented here, but these are the most likely error codes to appear when using CCAI.  For the full list of potential Twilio errors, feel free to check out the entire roster here on their own [documentation](https://www.twilio.com/docs/api/errors).
[block:parameters]
{
  "data": {
    "0-0": "21211",
    "0-1": "Invalid 'To' Phone Number",
    "1-0": "21408",
    "1-1": "Permission to send an SMS has not been enabled for the region indicated by the 'To' number",
    "2-1": "Message body is required",
    "3-1": "Attempt to send to unsubscribed recipient",
    "3-0": "21610",
    "4-0": "21704",
    "4-1": "The Messaging Service contains no phone numbers",
    "5-1": "Account suspended",
    "6-1": "Unreachable destination handset",
    "7-1": "Message blocked",
    "8-1": "Unknown destination handset",
    "9-1": "Landline or unreachable carrier",
    "10-1": "Carrier violation",
    "11-1": "Message filtered",
    "11-0": "30007",
    "10-0": "30007",
    "9-0": "30006",
    "8-0": "30005",
    "7-0": "30004",
    "6-0": "30003",
    "5-0": "30002",
    "2-0": "21602"
  },
  "cols": 2,
  "rows": 12
}
[/block]