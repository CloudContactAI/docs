---
title: Compliance
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
Data security and compliance has become a very hot topic of discussion, especially when it comes to digital protection of personal data on the web.  As such, it's our job at CloudContactAI to protect users as well as the users' clients. Going forward, laws will continue to shift in response to changing threats and we'll do all we can to keep our clients compliant with such laws. 

## Compliance Laws

## **CCPA**

The state of California introduced legislation for the California Consumer Privacy Act (CCPA) which took effect Jan 1, 2020. This bill intends to give Californians rights over the personal data companies collect. Companies have to disclose what information they collect, if they sell your information, and are required to provide an opt-out function.

## **GDPR**

In the European Union, they implemented a General Data Protection Regulation (GDPR) which took effect in May 2018. GDPR aims to bring all the EU member states under one umbrella by enforcing a single data protection law, intending to put guidelines and regulations on how data is processed, used, stored or exchanged.

## **TCPA**

The Telephone Consumer Protection Act (TCPA) was one of the first consumer protection laws enacted to protect consumers. This law created the basis of required telecom compliance. Companies cannot call consumers before 8 a.m. or after 9 p.m., maintain a do-not-call list, and must disclose their name/pertaining information.

## Settings

On the Settings menu item, there is a tab entitled TCPA Compliance for those who need to conform to the TCPA standards. Settings is only available on a paid plan.

![1360](https://files.readme.io/e503934-tcpa_compliance.png "tcpa_compliance.png")

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>

      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Do Not Contact anyone in the National Do Not Call Registry
      </td>

      <td>
        A lookup of the phone number is done against the National Do Not Call Registry. If the phone number resides in the Do Not Call Registry, then CCAI will not communicate with this contact via SMS or Voice.
      </td>
    </tr>

    <tr>
      <td>
        Enable Client Users to respond only with Templatized Messages
      </td>

      <td>
        This feature forces users of CCAI to respond with canned templatized messages only.
      </td>
    </tr>

    <tr>
      <td>
        Contacts will not be sent text messages before 8 am and after 9 pm based upon the area code of the Contact
      </td>

      <td>
        The area code of the phone number is looked up to determine the timezone. If the current time in the contact's timezone is before 8 am and after 9 pm, then the message will not be sent. The message can be requeued at a more appropriate time.
      </td>
    </tr>

    <tr>
      <td>
        Inbox
      </td>

      <td>
        This checkbox determines whether the user can send SMS messages in the Inbox outside of the 8 am to 9 pm window
      </td>
    </tr>

    <tr>
      <td>
        SMS Campaigns
      </td>

      <td>
        This checkbox determines whether the user can send SMS Campaigns outside of the 8 **am** to 9 pm window.
      </td>
    </tr>

    <tr>
      <td>
        API
      </td>

      <td>
        This checkbox determines whether the API can send SMS messages outside of the 8 **am** to 9 pm window.
      </td>
    </tr>
  </tbody>
</Table>
