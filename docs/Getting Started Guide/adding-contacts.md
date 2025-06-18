---
title: Adding Contacts
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Adding Contacts to your CloudContactAI account
  description: >-
    Import contacts into your CloudContactAI account using the file upload,
    SFTP, or the API
  image: >-
    https://files.readme.io/73d3dc6ba45362469e97b734c5057f3c54d14ff97b5fe1873e99705cdc549bbc-Group_14.png
  keywords:
    - sftp
    - file upload
    - api
    - sms
    - email
    - mms
  robots: index
next:
  description: ''
---
In CloudContactAI (CCAI), you can [add customer contact information](https://www.cloudcontactai.com/how-to-create-and-upload-contacts/) individually or in bulk.  This can be done with either:

* CSV Import
* Using the "Add Contact" option
* Contact API [endpoint](https://developer.cloudcontactai.com/reference/creates-a-contact) 

## CSV Import

To import contacts with a CSV file, navigate to the Contacts menu item on the menu bar. On the Contacts view, click on the Contact Lists tab. Select the Add Contacts button. 

![1412](https://files.readme.io/45d8a6a-Screenshot_2022-09-20_130617.png "Screenshot 2022-09-20 130617.png")

Leave the Upload CSV File radio button selected. Enter a name for your Contact List in the List Name edit control. Click on the Choose File button to upload your CSV file. 

![1091](https://files.readme.io/565ab6f-Screenshot_2022-09-20_130643.png "Screenshot 2022-09-20 130643.png")

CloudContactAI requires the following columns

* First Name - first\_name
* Last Name - last\_name
* Phone number - phone 
* Email - email

You can add columns to your CSV file in order to add additional properties to Contacts as needed. The column header will be the property name and the related cells are the values.

![793](https://files.readme.io/2e4ff6d-Screenshot_2022-09-20_130853.png "Screenshot 2022-09-20 130853.png")

## Using the "Add Contact" option

To add a single contact, navigate to the Contacts menu item on the menu bar. On the Contacts view, click on the Contacts tab. Select the Create Contacts button.  Select the Manually Add Contacts button. Enter First Name, Last Name, Phone, and Email. If you'd like to enter another contact, click the Add Contact button. Click on the Create button to create your Contacts.

![2050](https://files.readme.io/5799c0a-add_contact.png "add_contact.png")