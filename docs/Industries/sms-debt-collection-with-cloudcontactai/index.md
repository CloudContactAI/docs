---
title: SMS Debt Collection with CloudContactAI
excerpt: 'Step-by-step guide to setting up and sending SMS debt collection campaigns with CloudContactAI.'
deprecated: false
hidden: false
metadata:
  title: ''
  description: >-
    Debt Collection with CloudContactAI is quick and easy. Simple upload the
    account information and the amount do an CloudContactAI will render a
    payment portal for your end users
  image: >-
    https://files.readme.io/c75c70e1ea62f8f8904742dc062e1a9a49baba4447099049d281af992764c387-Group_84_1.png
  keywords:
    - debt collection
    - cloudcontactai
    - payment portal
  robots: index
next:
  description: ''
---
This guide will walk you through how to do SMS debt collection with CloudContactAI. Debt collection is typically divided into 4 buckets based upon Days Past Due (DPD): 1-30, 31-60, 61-90, and final. CloudContactAI provides templates and file formats for these buckets.

First, sign up for CloudContactAI by navigating to this [link](https://app.cloudcontactai.com/register). After you sign up, on the Welcome Dialog, click Add Contacts.

In CloudContactAI, the default CSV template to upload a list of contacts is not for Debt Collection. Please use this template, [test\_collections\_1-30dpd.csv](https://dev.cloudcontactai.com/wp-content/uploads/2022/12/test_collections_1-30dpd.csv).

In this template file, we’ve specified the following header and data rows:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Name
      </th>

      <th>
        Value
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        firstName
      </td>

      <td>
        Betty
      </td>
    </tr>

    <tr>
      <td>
        lastName
      </td>

      <td>
        Ruble
      </td>
    </tr>

    <tr>
      <td>
        amount
      </td>

      <td>
        30.00
      </td>
    </tr>

    <tr>
      <td>
        retailer
      </td>

      <td>
        Amazon
      </td>
    </tr>

    <tr>
      <td>
        orderNo
      </td>

      <td>
        123
      </td>
    </tr>

    <tr>
      <td>
        paymentLink
      </td>

      <td>
        [https://www.stripe.com](https://www.stripe.com)
      </td>
    </tr>

    <tr>
      <td>
        phoneNumber
      </td>

      <td>
        4158906431
      </td>
    </tr>

    <tr>
      <td>
        email
      </td>

      <td>
        [info@cloudcontactai.com](mailto:info@cloudcontactai.com)
      </td>
    </tr>

    <tr>
      <td>
        dueDate
      </td>

      <td>
        12/19/22
      </td>
    </tr>

    <tr>
      <td>
        creditorName
      </td>

      <td>
        The Collectors
      </td>
    </tr>
  </tbody>
</Table>

The field names match up to the messages that are in CCAI for you.

In the Add Contacts view, I’m going to upload the default collection template file. I’m going to entitle the list the name of the file “test\_collections\_1-30dpd.csv”.

![1059](https://files.readme.io/3ce61c6-cloudcontactai-debt-collection-template-add-contacts.png "cloudcontactai-debt-collection-template-add-contacts.png")

I’ll click the “Create” button, and then my Contact list will be uploaded. 

When I navigate to the Contact Lists tab, I’ll see my uploaded list. 

![2204](https://files.readme.io/f6f2f87-cloudcontactai-debt-collection-template-add-contact-list.png "cloudcontactai-debt-collection-template-add-contact-list.png")

When I click on the uploaded Contact List in the UI, I’ll be taken to the only contact that we uploaded, Betty Rubble. When I click on Betty Rubble, I’ll see Betty’s contact details. What’s interesting with Betty’s contact details is not only are we showing the standard fields: First Name, Last Name, Phone, and email, but were also showing amount, creditorName, dueDate, orderNo, paymentLink, and retailer. CloudContactAI is really flexible when it comes to storing contact details. You just need to include the field definitions in the header row, and we’ll store it as a contact detail. For example, if I wanted to import the field ZipCode, then I would have added another field to the header row entitled ZipCode, and another field value, e.g. 94127, to Betty Rubble’s data row. It’s that simple.

![1523](https://files.readme.io/fb114bb-cloudcontactai-debt-collection-template-contact-details.png "cloudcontactai-debt-collection-template-contact-details.png")

Now, that I’ve got Betty loaded, let’s send her a text to see if I can collect on the $ she owes us. Click on the SMS Campaign. Click on Create SMS Campaign. On the New Campaign view, let’s call the campaign “SMS 1-30DPD”. Let’s specify that we’re going to send to the contact list that we just uploaded. 

![1097](https://files.readme.io/2607a4a-cloudcontactai-debt-collection-template-sms-campaign.png "cloudcontactai-debt-collection-template-sms-campaign.png")

In the Message section, we’ll specify the Industry as Debt Collection. For Messages, we’ll specify “1-30 Days Past Due (DPD)”. Notice that the Contact Fields have the same tags as the fields that were uploaded with the default debt collection template. These fields will be evaluated dynamically when we launch the campaign.

![1080](https://files.readme.io/da1d9ed-cloudcontactai-debt-collection-template-sms-campaign-2.png "cloudcontactai-debt-collection-template-sms-campaign-2.png")

Click on the Send SMS Campaign button. Click through the dialogs, and your campaign will be launched. On the subsequent Campaigns view, click on the “SMS 1-30 DPD” campaign. You’ll be able to see the message that was sent to Betty Rubble with the tags evaluated. 

![1837](https://files.readme.io/2ae00d1-cloudcontactai-debt-collection-template-sms-campaign-3.png "cloudcontactai-debt-collection-template-sms-campaign-3.png")

Betty will receive an SMS that looks like

![971](https://files.readme.io/51499e3-cloudcontactai-debt-collection-template-sms-campaign-4.png "cloudcontactai-debt-collection-template-sms-campaign-4.png")

When Betty responds back to your SMS outreach, your Inbox will populate.

![2209](https://files.readme.io/a59ab13-cloudcontactai-debt-collection-template-sms-campaign-5.png "cloudcontactai-debt-collection-template-sms-campaign-5.png")

You can either respond to Betty, assign one of your colleagues to respond to Betty, set up an auto response, or ignore Betty. If Betty responds with Stop, she'll be immediately moved from any subsequent SMS messages.

To download the results from you campaign, navigate to Reports. Click on the SMS Campaign Report Tab. Click on the Download Campaign Results.

We'll tackle SMS 31-60 DPD in our next post.