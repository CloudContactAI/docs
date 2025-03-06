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
[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fwww.youtube.com%2Fembed%2Fv46gYmbB-yM%3Ffeature%3Doembed&display_name=YouTube&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3Dv46gYmbB-yM&image=https%3A%2F%2Fi.ytimg.com%2Fvi%2Fv46gYmbB-yM%2Fhqdefault.jpg&key=02466f963b9b4bb8845a05b53d3235d7&type=text%2Fhtml&schema=youtube\" width=\"854\" height=\"480\" scrolling=\"no\" title=\"YouTube embed\" frameborder=\"0\" allow=\"autoplay; fullscreen; encrypted-media; picture-in-picture;\" allowfullscreen=\"true\"></iframe>",
  "url": "https://www.youtube.com/watch?v=v46gYmbB-yM",
  "title": "How to Manage Contacts",
  "favicon": "https://www.google.com/favicon.ico",
  "image": "https://i.ytimg.com/vi/v46gYmbB-yM/hqdefault.jpg",
  "provider": "https://www.youtube.com/",
  "href": "https://www.youtube.com/watch?v=v46gYmbB-yM",
  "typeOfEmbed": "youtube"
}
[/block]


<br />

When adding contacts to CCAI's contact lists, there is also the option to add custom properties as well. This is incredibly useful for keeping customers segmented and categorized, which is incredibly useful for:

- Selecting a specific group of customers for a Campaign.
- Searching for message threads of customers associated with a certain property.
- Storing information about your customers.

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

- 4432, 30011 -- Messaging to country are forbidden
- 4433 -- Messaging to Toll Free numbers are forbidden
- 4435 -- Too many recipients
- 4481 -- From number in black list
- 4482 -- To number in black list
- 4493 -- Unauthorized
- 4700, 30006 -- Carrier Rejected as Invalid Service Type
- 4720, 30005 -- Carrier Rejected as Invalid Destination Address
- 4750 -- Carrier Rejected Message
- 4770 -- Carrier Rejected as SPAM
- 4775 -- Carrier Rejected due to user opt out