---
title: Delivery Details
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
[block:api-header]
{
  "title": "CCAI Delivery System"
}
[/block]
With CloudContactAI, campaigns and messages are intentionally delayed to reduce the likelihood of carriers blocking due to spam. We utilize A2P (application to person) protocols for sending messages to improve deliverability rates. Additional, there are toll-free, short code, and local numbers on offer which helps increase deliverability. Users will also be notified if the message made it to the customer’s device with full visibility on the status of the message to see if it’s in queue, sent, delivered, or possibly experienced an error.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e638a87-Screenshot_2022-10-14_094256.png",
        "Screenshot 2022-10-14 094256.png",
        677,
        133,
        "#000000"
      ],
      "caption": ""
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "What is Deliverability Rate?"
}
[/block]
SMS deliverability is a measure of the percentage of outgoing text messages which are received at their intended destination. There are a lot of criteria that determines whether or not your message will be delivered. Different carriers evaluate messages at their discretion, and the rules they use can change at any time. But, in general, they look at a common set of criteria when deciding whether or not to allow your messages on their network.
[block:api-header]
{
  "title": "Message Status"
}
[/block]
There are four main status states for outgoing campaigns.

  * Sent - The campaign has gone through and is viewable by the recipient.
  * Error - Something has gone awry, whether it be the contact's number is not valid, the user is blocked, or the campaign was denied by administration.  For the full list of potential reasons, check out the section on Deliver Error Codes.
  * Scheduled - This is when the user has set the campaign to launch at a specific time as opposed to the moment they send it.
  * Awaiting Validation - The campaign is being sent to either more than one client and/or is being sent with a URL that administration will need to validate is safe in order to prevent spam, scams, and phishing.
[block:api-header]
{
  "title": "Messaging Critereon"
}
[/block]
## **The Sender**

  * Who is the sender?
  * What number are they using?
  * Have either been flagged for SPAM in the past?
 
## **How They Are Sending**

  * What type of number are they sending from?
  * Are they sending person-to-person or high-volume, application-to-person (A2P) messages?

## **The Volume of Messages Being Sent**

  * How many total messages are being sent?
  * How many messages are being sent per second?

## **Message Content**

  * Does the message include links?
  * Does it use the link shortener?
  * Does it contain suspicious phrases or illicit content? 
[block:api-header]
{
  "title": "Pointers for Message Deliverability"
}
[/block]
  * Make sure any two variants of campaign are sufficiently different from each other.
  * Try to personalize messages to the customer. Include properties like the customer’s first name by including: {first_name}
  * Be as colloquial as possible. The more machine-like the message sounds, the lower the response rates.
  * Try to mass message customers only after they’ve messaged back indicating they like text as a channel.
  * When you have to reach out first, introduce yourself as a person (“Hey, this is Dolan from CloudContactAI” vs “Hey this is CloudContactAI”)