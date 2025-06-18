---
title: CSV import or export
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Importing and Exporting CSV files with CloudContactAI
  description: >-
    You can use the CloudContactAI UI to import and export CSV files. If you're
    looking for more complicated ETL, then please contact support to either make
    use of our SFTP or API services.
  image: >-
    https://files.readme.io/a0c292a7e938fa82bd47987f42bec4a019e15976a03440ad593d3e503ebefbbb-Group_84_1.png
  keywords:
    - import csv
    - export csv
    - sftp
    - API
  robots: index
next:
  description: ''
---
As described back in the chapter about managing customer info, our CSV file is a really good way of uploading several customers, especially if their credentials have already been saved on another file.  Alternatively, if they need to be exported for other purposes, they can be downloaded as a CSV file.

## Importing Contacts

Under the Contacts tab, most of everything will be done from the '+ Add Contacts' option under the Contacts Lists sub-tab.  

![1642](https://files.readme.io/541b571-Screenshot_2022-10-13_113420.png "Screenshot 2022-10-13 113420.png")

The first option along the subsequent sent of radio buttons is where importing CSV files takes place.  The template can be downloaded as 'example.csv' with all the categories already established.  Note: there are categories other than first\_name, last\_name, and phone, but they aren't required for the file to be uploaded.

![1117](https://files.readme.io/fdbc163-Screenshot_2022-10-13_113730.png "Screenshot 2022-10-13 113730.png")

## Adding Variables

While the CSV document or the page where the template is downloaded doesn't state it explicitly, we do allow users to add additional variables following the first name, last name, and phone number.

As shown below, this is the template CSV that is provided on CCAI.

![628](https://files.readme.io/0b33c51-Screenshot_2022-11-03_095509.png "Screenshot 2022-11-03 095509.png")

Let's say for example that these are clients who visited different branches of the user's company and campaigns that are being sent need to advertise the branch that is most likely closest to where these customers live.  The user would then add a new variable in the first column 'store\_branch.'

![428](https://files.readme.io/8b38a0a-Screenshot_2022-11-03_101206.png "Screenshot 2022-11-03 101206.png")

From here, it's a matter of filling out the new column appropriately and uploading the saved CSV as normal.

## Exporting Contacts