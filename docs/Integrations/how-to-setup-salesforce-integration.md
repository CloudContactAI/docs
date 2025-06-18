---
title: 'Salesforce: How to Setup Integration'
excerpt: >-
  This is an overview of how to install and implement CloudContactAI's
  Salesforce Integration. Our dedicated Partner Experience Team is more than
  happy to walk you through the steps if you need assistance.
deprecated: false
hidden: false
metadata:
  title: 'CloudContactAI''s Salesforce Integration '
  description: ''
  image: >-
    https://files.readme.io/8d71e8d9fe5dfd515b6fd19b640d0f82f7b7b0b7dae5f04c65ec72ddddc89e28-CCAI_800x800.png
  keywords:
    - salesforce
    - cloudcontactai
  robots: index
next:
  description: ''
---
## Install Package

1. Select Users who will have access to this package
2. Click the acknowledgment option
3. Select ‘Upgrade’ / ‘Add’ to add the package to your SFDC instance

<Image align="center" src="https://files.readme.io/c94e2c3-salesforce1.png" />

## Update Apex Settings

1. Click the ‘Deploy Metadata from Non-Certified Package Versions via Apex’
2. Click Save

<Image align="center" src="https://files.readme.io/4d31f96-salesforce2_copy.jpeg" />

## Update Connected Apps

1. Go to Setup
2. Search and Click ‘Manage Connected Apps’
3. Edit ‘CloudContactAI OAuth’
4. Update IP Relaxation to ‘Enforce IP restrictions, but relax for refresh tokens’
5. Update Refresh Token Policy to ‘Refresh Token is valid until revoked’

<Image align="center" src="https://files.readme.io/2312164-salesforce3.png" />

## CloudContactAI / SFDC Connection

1. Select Environment (Production or Sandbox)
2. Each CloudContactAI account has a publishable key and private token; Add those to the CloudContactAI Company Token area
3. Check the connection
4. If Connection is good, click ‘Authorize.’ Authorize allows for SMS messages to sync back to SFDC objects as tasks
5. Click Save

<Image align="center" src="https://files.readme.io/382732a-salesforce4.png" />

## CloudContactAI / SFDC Property Mapping

1. CloudContactAI out of the box can pull data from any properties on the Lead, Contact, and Opportunity pages within SFDC
2. The Property Manager page allows you to select which pieces of data you want to send to CloudContactAI from SFDC
3. The Property Sync Enabled toggle is important to have enabled to sync these fields
4. Click Save when finished mapping

<Image align="center" src="https://files.readme.io/28eb906-salesforce5.png" />

## Setup Send Text Button

### Salesforce Lightning

1. Send Text button can be added to the Lead, Contact, and Opportunity Page.
2. Locate and edit your desired Page Layout
3. Select ‘Mobile & Lightning Actions’ from the layout options
4. Click and drag the ‘Send Text’ button to the designated area. The order that you place these buttons will determine the order of buttons on a lightning page.
5. Save Layout

<Image align="center" src="https://files.readme.io/930a394-salesforce6_copy.jpeg" />

### Salesforce Classic

1. Send Text button can be added to the Lead, Contact, and Opportunity Page.
2. Locate and edit your desired Page Layout
3. Select ‘Buttons’ from the layout options
4. Click and drag the ‘Send Text’ button to the designated area
5. Save Layout

<Image align="center" src="https://files.readme.io/1425708-salesforce7_copy.jpeg" />