---
title: How to associate a new SMS Message with an Existing Campaign
excerpt: >-
  In certain situations, the end user may want to associate a new SMS message
  with an existing Campaign.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  image: >-
    https://files.readme.io/14fadfde917fcbf9ffd26ed0eff5a362c87522e84cd322ef398fba712cbec103-Group_84_1.png
  keywords:
    - api
    - sms message
    - api
    - cloudcontactai
  robots: index
next:
  description: ''
---
1. Create a Campaign 
2. Take the campaignID from the Campaign. 
3. POST to this URL replacing \{clientId} and \{campaignID} accordingly.  [https://core.cloudcontactai.com/api/clients/\{clientId}/campaign/\{campaignId}/message](https://core.cloudcontactai.com/api/clients/\{clientId}/campaign/\{campaignId}/message) 
   ```json
   {
       "message": "Hello, ${firstName}",
       "account": {
           "firstName":"hon",
           "lastName":"Doe",
           "phone":"+14155551212"
       }    
   }
    
   ```
4. CloudContactAI should respond with a 200. 
   ```json
   {
       "status": "success"
   }
    
   ```