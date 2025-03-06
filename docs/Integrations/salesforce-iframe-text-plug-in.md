---
title: 'Salesforce: iFrame Text Plug-In'
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
This integration is an extension of CloudContactAI placed conveniently within your contact pages in Salesforce. It simultaneously syncs your contact’s number, conversation history, and properties directly into both Salesforce and CloudContactAI. You get all the functionality of CloudContactAI's text messaging platform and tagging capabilities right within your main sales tool.

# iFrame In Use

## Desktop

<Image align="center" src="https://files.readme.io/813d6d7-salesforce10.png" />

# iFrame Setup (Lightning Only)

1. Search ‘Lightning App Builder’ in Setup
2. Click ‘Edit’ on the Page you wish to add an iFrame to

<Image align="center" src="https://files.readme.io/0fb1e13-salesforce11.png" />

3. From the middle section of the page, find where you want to add the iFrame and select that section
4. Add a new tab in that section
5. Make the new tab label Custom and title whatever you wish. We recommend "CloudContactAI SMS"
6. Drag and drop the CloudContactAI chat into that newly created section
7. Click on the CloudContactAI Chat section you just dropped into place
8. Select whether this is using the CloudContactAI Sandbox OR Production Environment
9. Activate the layout
10. Save the layout

## CloudContactAI Chat Canvas

1. Navigate to Setup > Apps > App Manager > CloudContactAI Chat Canvas > Manage > Edit Policies 
2. Update the OAuth Policies Permitted.
3. Select Manage Profiles
4. Then select all the profiles that need access to the iFrame
