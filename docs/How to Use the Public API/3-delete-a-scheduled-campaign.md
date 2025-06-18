---
title: Delete a Scheduled Campaign with the CloudContactAI API
excerpt: >-
  In this tutorial, we'll show you how to delete a scheduled campaign. This
  article assumes that you completed steps 1 and 2 of How to use the Public API
deprecated: false
hidden: false
metadata:
  title: >-
    How to delete a scheduled SMS campaign with Postman and CloudContactAI using
    the API
  description: ''
  image: >-
    https://files.readme.io/0721d10ee4e8c114fbcd88c6d5802ea1e56f1eac6d7f89b714448538063dcc47-Group_84_1.png
  keywords:
    - api
    - delete campaign
    - scheduled campaign
    - cloudcontactai
    - api
  robots: index
next:
  description: ''
---
1. In the Postman collection that you downloaded from [here](https://www.cloudcontactai.com/wp-content/uploads/2024/01/CCAI.Campaigns.postman_collection.json_.zip), click on the Delete a Campaign function 
2. ![](https://files.readme.io/0e49044-image.png)

   In the address bar, you'll see the URL that we're going to invoke to delete a campaign. The coreURL will be picked up from your Environment Variable. The campaignId will need to be specified as a Collection Variable.  This is different from the Environment Variable because this variable can change within the Environment. In step 2 of How to use the Public API, the response body from the creation of the campaign contained an "id", this is the campaign id. This is the "id" specified below. 
3. ![](https://files.readme.io/a36aab6-image.png)

   Click on the Campaigns Collection in Postman.
4. Cli the Variables tab
5. Enter the campaignId
6. ![](https://files.readme.io/bd9b42b-image.png)

   Hit the Save button. 
7. Navigate back to the Delete REST API invocation in Postman. 
8. ![](https://files.readme.io/63506eb-image.png)

   Hit the Send button 
9. You should receive a 200 OK back from the server 
10. ![](https://files.readme.io/209b9c8-image.png)
11. Navigate back to [CCAI](https://www.cloudcontactai.com)
12. Click on SMS Campaigns
13. Click on Scheduled Campaigns
14. Your Scheduled Campaign should be gone
15. ![](https://files.readme.io/8d84507-image.png)