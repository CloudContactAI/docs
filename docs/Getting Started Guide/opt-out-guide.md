---
title: Opt-Out Messages
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Opt-Out of receiving messages with CloudContactAI
  description: >-
    Users can opt-out of receiving messages from CloudContactAI to stop
    receiving messages.
  image: >-
    https://files.readme.io/a25aabebb0bdcf7849c308c47afeff466f34c3e896633b6855aa8d579c209423-Group_14.png
  keywords:
    - opt-out
    - sms
    - cloudcontactai
  robots: index
next:
  description: ''
---
## Opt-Out Messages

This guide is designed to help explain opt-out messages, their importance, as well as some best practices for your business. For a more complete understanding, please read the "Opt-In Messages" before reading this guide on opt-out messages. For specifications and additional information it is best to consult an attorney to ensure that you are in compliance with current regulations.

**opt**\
*verb*\
intransitive verb\
: to make a choice\
especially : to decide in favor of something

![3772](https://files.readme.io/9d6b6ee-pexels-cottonbro-studio-3825275.jpg "pexels-cottonbro-studio-3825275.jpg")

**What is an Opt-out message?**

When CloudContactAI send an SMS Message to a Contact, the Contact can Opt-out by sending back any of the following keywords: .STOP, STOPALL, UNSUBSCRIBE, CANCEL, END, or QUIT.

Any of these STOP keyword replies will prevent a customer from receiving new messages from the phone number they're responding to. 

In addition, CloudContactAI will update the Contact to state that the Contact has opted-out. 

Alternatively, if you receive a message that is not one of these 6 words, but you're pretty sure that the end user wants to opt-out. You can navigate to the Contact in CloudContactAI, and select the Do Not Text button on the Contact Information. Once this checkbox is selected, then no SMS messages will be delivered to this Contact.

![1869](https://files.readme.io/49e43ad-do_not_text.png "do_not_text.png")

Another strategy is to create a new tab in the Inbox called Stop or Unsubscribe. Messages can then be moved to the Stop tab. You can then update all of the Messages' Contacts to Do Not Text.

![619](https://files.readme.io/5bf80ef-stop_tab.png "stop_tab.png")

You can also create a Keyword at the phone number level that routes a Message that contains the keyword to the Stop tab. 

![2066](https://files.readme.io/fdc38ee-automatic_keyword.png "automatic_keyword.png")