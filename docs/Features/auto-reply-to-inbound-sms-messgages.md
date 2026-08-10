---
title: Auto-Reply to Inbound SMS Messgages
excerpt: >-
  CloudContactAI provides an easy mechanism to auto-reply to inbound SMS
  messages
deprecated: false
hidden: false
metadata:
  title: Auto-Reply to Inbound SMS Messages without an Agent
  description: 'Configure auto-reply messages for inbound SMS in CloudContactAI. Set keyword triggers, custom responses, and opt-in actions per phone number.'
  image: >-
    https://files.readme.io/bad0be854d50f33df558cf713c25155af9af61686194006adbe487e1ad19d188-Group_14.png
  keywords:
    - auto-reply
    - sms inbound
    - cloudcontactai
  robots: index
next:
  description: ''
---
CloudContactAI supports the ability to respond to inbound SMS messages at the level of the phone number. This means that if you have multiple phone numbers, you can configure the auto-replies to be different for each phone number.

To auto-reply to inbound messages

1. Navigate to the Phone Numbers menu item. 

![](https://files.readme.io/158f388-image.png)

2. Click on the Edit Pencil of the phone number that you would like to change the auto-reply. 
3. ![](https://files.readme.io/33e7903-image.png)

   Now, you have a couple of options to configure an Auto-Reply
4. To respond to all inbound SMS messages with the same message, click on the checkbox, and type your automated response

![](https://files.readme.io/f0ef886-image.png)

5. To respond to a specific keyword, type the keyword into the Keywords section

![](https://files.readme.io/b9758aa-image.png)

6. After you specify the keyword, you can then specify an action. 
7. The following actions are supported:
   1. Response Message - The response message is typically text with a URL
   2. Add Contact to Dynamic Segment - This is useful for building an Opt-In list. Ask users to text your phone number a specific keyword. When users text the keyword, they will be added to a Dynamic Segment list that you can use in a subsequent campaign
   3. Unsubscribe - Users will type the specific keyword as a response, and CloudContactAI will route them through the unsubscribe mechanism
   4. Subscribe - Users will type the specific keyword as a response, and CloudContactAI will route them through the subscribe mechanism

![](https://files.readme.io/418f32d-image.png)

8. Click on the Update button to save your changes for Auto-Replies.