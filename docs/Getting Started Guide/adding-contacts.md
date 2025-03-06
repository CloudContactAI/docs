---
title: Adding Contacts
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
In CloudContactAI (CCAI), you can [add customer contact information](https://www.cloudcontactai.com/how-to-create-and-upload-contacts/) individually or in bulk.  This can be done with either:

  * CSV Import
  * Using the "Add Contact" option
  * Contact API [endpoint](https://developer.cloudcontactai.com/reference/creates-a-contact) 

## CSV Import 

To import contacts with a CSV file, navigate to the Contacts menu item on the menu bar. On the Contacts view, click on the Contact Lists tab. Select the Add Contacts button. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/45d8a6a-Screenshot_2022-09-20_130617.png",
        "Screenshot 2022-09-20 130617.png",
        1412,
        228,
        "#000000"
      ]
    }
  ]
}
[/block]
Leave the Upload CSV File radio button selected. Enter a name for your Contact List in the List Name edit control. Click on the Choose File button to upload your CSV file. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/565ab6f-Screenshot_2022-09-20_130643.png",
        "Screenshot 2022-09-20 130643.png",
        1091,
        440,
        "#000000"
      ]
    }
  ]
}
[/block]
CloudContactAI requires the following columns
  * First Name - first_name
  * Last Name - last_name
  * Phone number - phone 
  * Email - email

You can add columns to your CSV file in order to add additional properties to Contacts as needed. The column header will be the property name and the related cells are the values.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2e4ff6d-Screenshot_2022-09-20_130853.png",
        "Screenshot 2022-09-20 130853.png",
        793,
        376,
        "#000000"
      ]
    }
  ]
}
[/block]
## Using the "Add Contact" option 

To add a single contact, navigate to the Contacts menu item on the menu bar. On the Contacts view, click on the Contacts tab. Select the Create Contacts button.  Select the Manually Add Contacts button. Enter First Name, Last Name, Phone, and Email. If you'd like to enter another contact, click the Add Contact button. Click on the Create button to create your Contacts.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5799c0a-add_contact.png",
        "add_contact.png",
        2050,
        683,
        "#000000"
      ]
    }
  ]
}
[/block]