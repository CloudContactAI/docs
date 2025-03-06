---
title: Reassigned Phone Number Lookup
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
Before sending an SMS message with CloudContactAI, you can have CloudContactAI look up the contact's phone number to see if the phone number is in the Reassigned Phone Number database. The Reassigned Phone Number database tracks phone numbers that were recently unsubscribed. If the phone number is in the Reassigned Phone Number database, then CloudContactAI will NOT text the phone number. 

The Reassigned Phone Number configuration is enabled and disabled at the CloudContactAI account level. If the feature is enabled, CloudContactAI will do the Reassigned Phone Number database lookup when attempting to send the SMS message. When the lookup is performed, then the lookup is valid for 60 days. This means that CloudContactAI will not do the lookup again until 60 days have elapsed. 

With the Reassigned Phone Number Database active for a CloudContactAI account, the user can now inspect the Reassigned Status by looking at the Contact Details page.  Under the phone number category, there is a new label describing the last time the database was referenced using that number right below it.

<Image align="center" src="https://files.readme.io/94c3915da67dce32c20f4f5740098ad6efe0ebe97a00ec3149be0232c21be1c1-last_reassigned_not_triggered.png" />

Attempting to send a message to a recently reassigned number will cause an error and CCAI will not send a message to the number within the established duration for the account.  After the duration has ended, the number can then be messaged again, though it will have a new user that must be considered.

In addition, you can use the Contact API endpoint to view the status of the Reassigned Phone Number Lookup. 

**Technical Details**

When a new SMS message request comes in, we will do the Reassign Phone Number lookup if the lookup has not been done in the last 60 days. We will write the timestamp of the Lookup request to the Contact.lastReassignLookupTimestamp field. If the number has been reassigned, we will not send the message to the contact. We will write the timestamp for this success to the Contact.reassignedAtTimestamp field.

Here are the results from a phone number that has recently been reassigned. The phone number is 775-772-1010. This is a real-world example.

Here is the CURL request. 

curl --request GET\
     \--url [https://core.cloudcontactai.com/api/v2/contacts/672b99f36b065668b903d8cc%20](https://core.cloudcontactai.com/api/v2/contacts/672b99f36b065668b903d8cc%20) 

The JSON that you get back from invoking our Contact API will look like this

\{\
  "id": "672b99f36b065668b903d8cc",\
  "clientId": "2351",\
  "phone": "7757721010",\
  "phoneInfo": \{\
    "phoneNumber": "7757721010",\
    "phoneType": "MOBILE",\
    "carrierName": "T-Mobile USA, Inc.",\
    "phoneUnsubscribedSince": null,\
    "phoneManuallyUnsubscribed": false,\
    "**lastReassignLookupTimestamp**": 1730910708422,\
    "**reassignedAtTimestamp**": 1730910708422\
  },
