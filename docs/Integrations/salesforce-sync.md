---
title: 'Salesforce: Sync'
excerpt: >-
  Many companies need to maintain all customer data in one place. With our
  Salesforce integration, you'll be able to automatically keep Salesforce up to
  date with customers and messages from CloudContactAI.
deprecated: false
hidden: false
metadata:
  title: ''
  description: 'Sync contacts and SMS conversations between Salesforce and CloudContactAI automatically. Matches by phone number with hourly updates.'
  robots: index
next:
  description: ''
---
# Data Syncing

All CCAI contacts will be matched by phone numbers with Salesforce contacts. When someone uses our SFDC package, they will utilize property mapping to match a phone number from a contact, lead, or opportunity into a customer record on CCAI. For each match, it will sync all messages from CCAI, segmented by day, as well as all selected data about the contact in Salesforce.

When a match happens, CCAI receives a Salesforce ID for the record it was mapped from. Then, when a conversation takes place and someone closes the respective thread in CCAI, it will create an SFDC log of all the back-and-forth messages from the beginning to the end of the conversation.

Each data sync is done at the 20-minute mark of every hour (9:20, 10:20, 11:20, etc.). The integration will do a bulk upload of all conversations and new properties that took place during that hour.
