---
title: Delivery Message Receipt for SMS Messages
excerpt: >-
  CloudContactAI provides a Delivery Message Receipt Mechanism for SMS Messages.
  You can verify if the Messages were delivered by other Conversations
  Participants.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
1. Login to CloudContactAI
2. Navigate to the Settings Tab of a Paid Account
3. Click on the Integration Tab
4. ![](https://files.readme.io/94fecf786e5e976d6f3926ea394dffd4d09f0a5f5bee98b9802897eabc66b163-image.png)

   The second SMS Callback is used for Delivery Messages Receipts. You'll need to configure your application to receive this callback via a PUT or POSTfrom CCAI. 
5. Your callback will receive a JSON block.

   ```json
   {
     "smsSid": 12345,
     "totalPrice": 0.12,
     "to": "+199999999",
     "messageStatus": "SENT",
     "segments": 4
   }
    
   ```
