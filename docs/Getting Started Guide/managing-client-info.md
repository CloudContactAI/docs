---
title: Managing Contact Info
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
<Embed url="https://www.youtube.com/watch?v=v46gYmbB-yM" title="How to Manage Contacts" favicon="https://www.google.com/favicon.ico" image="https://i.ytimg.com/vi/v46gYmbB-yM/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/watch?v=v46gYmbB-yM" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252Fv46gYmbB-yM%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253Dv46gYmbB-yM%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252Fv46gYmbB-yM%252Fhqdefault.jpg%26key%3D02466f963b9b4bb8845a05b53d3235d7%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

<br />

When adding contacts to CCAI's contact lists, there is also the option to add custom properties as well. This is incredibly useful for keeping customers segmented and categorized, which is incredibly useful for:

* Selecting a specific group of customers for a Campaign.
* Searching for message threads of customers associated with a certain property.
* Storing information about your customers.

![](https://files.readme.io/19cdb6f-Screenshot_2022-09-20_134516.png "Screenshot 2022-09-20 134516.png")

## Modifying Contacts

Customer properties can be modified through a number of ways.  This can be done either individually or in bulk if it is a variable that can be applied to multiple contacts.

## Uploading CSV File

In the template CSV file we provide in the 'upload customer' option, there are a number of categories that can be filled out for both categorization and additional factors beyond name and contact information.  These aren't necessary for the file to be accepted upon uploading.  If the customer is already saved to your list of contacts, any changes in variables that have been made compared to what is kept on CCAI will override any existing variables.

![](https://files.readme.io/bf86285-Screenshot_2022-09-20_134545.png "Screenshot 2022-09-20 134545.png")

## Changing Contact Info Individually

If a customer status needs to be changed or there's something unique about a certain customer, it's possible to go to the contact list their name is kept under and change by clicking on it.  The same variables from the CSV file appear here.

## Adding Modifications to Multiple Customers

From the top of a contact list alongside the search bar, there's several options to apply different categories to multiple contacts.  You just set what variable you want to apply, click on the checkboxes that the changes are to be applied to, and click 'accept.'

## How this all Works

Under the Inbox page, there are a couple ways these are utilized.  With the choice of multiple tabs, each can be modified to hold only customers with select variables applied for ease of organization. 

Alternatively, using the search bar, you can search by the variables applied.

## System Properties

System properties are automatically set by our platform on the individual user level to enable specific functionality. Although these fields are editable (just as custom properties are), we recommend you don’t tweak the values of properties that are not created by you to ensure it can continue to function as intended.

Current system properties used are:

**Delivery Failed** – This property indicates to the system that the most recent message to that customer failed to deliver. Customers with the following error codes are listed as follows:

* 4432, 30011 -- Messaging to country are forbidden
* 4433 -- Messaging to Toll Free numbers are forbidden
* 4435 -- Too many recipients
* 4481 -- From number in black list
* 4482 -- To number in black list
* 4493 -- Unauthorized
* 4700, 30006 -- Carrier Rejected as Invalid Service Type
* 4720, 30005 -- Carrier Rejected as Invalid Destination Address
* 4750 -- Carrier Rejected Message
* 4770 -- Carrier Rejected as SPAM
* 4775 -- Carrier Rejected due to user opt out
