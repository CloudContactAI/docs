---
title: Delivery Error Codes
excerpt: 'Reference guide for internal CCAI and carrier error codes when SMS delivery fails.'
deprecated: false
hidden: false
metadata:
  title: Error Codes with CloudContactAI
  description: >-
    CloudContactAI renders error codes from the platform and the carriers when
    rendering why a SMS message did not get sent.
  image: >-
    https://files.readme.io/497444768448e8ab31257da8a14c52449c45fdb64376adf3e66ada708f59b874-CCAI_800x800.png
  keywords:
    - error codes
    - sms messages
    - cloudcontactai
  robots: index
next:
  description: ''
---
![772](https://files.readme.io/c147217-Screenshot_2022-10-14_092031.png "Screenshot 2022-10-14 092031.png")

Whenever users look at a campaign that failed to go out, and the associated error code that comes tied with it when the cursor hovers over the error icon.  Here are what those codes mean.

## Internal Errors

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
        CCAI-ERR-00
      </td>

      <td>
        Phone validation error
      </td>
    </tr>

    <tr>
      <td>
        CCAI-ERR-01
      </td>

      <td>
        Landline
      </td>
    </tr>

    <tr>
      <td>
        CCAI-ERR-02
      </td>

      <td>
        Carrier Stated Landline
      </td>
    </tr>

    <tr>
      <td>
        CCAI-ERR-03
      </td>

      <td>
        Invalid Phone Number
      </td>
    </tr>

    <tr>
      <td>
        CCAI-ERR-10
      </td>

      <td>
        SMS Quota Exceeded
      </td>
    </tr>

    <tr>
      <td>
        CCAI-ERR-1
      </td>

      <td>
        Unexpected
      </td>
    </tr>

    <tr>
      <td>
        2001
      </td>

      <td>
        User asked to not text them (OptOut error)
      </td>
    </tr>

    <tr>
      <td>
        1000
      </td>

      <td>
        This account has exceeded trial SMS limit
      </td>
    </tr>

    <tr>
      <td>
        1001
      </td>

      <td>
        This client has exceeded monthly SMS limit
      </td>
    </tr>
  </tbody>
</Table>

## Common Twilio Errors

There are many more than documented here, but these are the most likely error codes to appear when using CCAI.  For the full list of potential Twilio errors, feel free to check out the entire roster here on their own [documentation](https://www.twilio.com/docs/api/errors).

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
        21211
      </td>

      <td>
        Invalid 'To' Phone Number
      </td>
    </tr>

    <tr>
      <td>
        21408
      </td>

      <td>
        Permission to send an SMS has not been enabled for the region indicated by the 'To' number
      </td>
    </tr>

    <tr>
      <td>
        21602
      </td>

      <td>
        Message body is required
      </td>
    </tr>

    <tr>
      <td>
        21610
      </td>

      <td>
        Attempt to send to unsubscribed recipient
      </td>
    </tr>

    <tr>
      <td>
        21704
      </td>

      <td>
        The Messaging Service contains no phone numbers
      </td>
    </tr>

    <tr>
      <td>
        30002
      </td>

      <td>
        Account suspended
      </td>
    </tr>

    <tr>
      <td>
        30003
      </td>

      <td>
        Unreachable destination handset
      </td>
    </tr>

    <tr>
      <td>
        30004
      </td>

      <td>
        Message blocked
      </td>
    </tr>

    <tr>
      <td>
        30005
      </td>

      <td>
        Unknown destination handset
      </td>
    </tr>

    <tr>
      <td>
        30006
      </td>

      <td>
        Landline or unreachable carrier
      </td>
    </tr>

    <tr>
      <td>
        30007
      </td>

      <td>
        Carrier violation
      </td>
    </tr>

    <tr>
      <td>
        30007
      </td>

      <td>
        Message filtered
      </td>
    </tr>
  </tbody>
</Table>