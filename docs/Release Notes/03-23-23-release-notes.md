---
title: (03-23-23) Release Notes
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
<Table align={["left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Jira Ticket
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1201
      </td>

      <td style={{ textAlign: "left" }}>
        The auto response checkbox on a phone number in the settings tab is now more properly aligned with the other lines.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1102
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed issue when importing a CSV file of contacts, if there is a column with empty variables that aren't the first name, last name, or phone number, the upload won't fail.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1022
      </td>

      <td style={{ textAlign: "left" }}>
        Added block inbound calls/text messages checkbox on contact settings.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1238
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed issue where putting in an invalid time when scheduling an SMS or email campaign would completely prevent launching the campaign regardless of whether the date had been changed to a valid value.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1239
      </td>

      <td style={{ textAlign: "left" }}>
        Duplicate of CLOUD-1238.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1032
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed issue where an error would occur when launching a campaign and using the "+ add contacts" option.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1220
      </td>

      <td style={{ textAlign: "left" }}>
        Added an automated email that alerts the user in the case of a failed CSV upload.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1212
      </td>

      <td style={{ textAlign: "left" }}>
        Increased character limit of the email title.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1221
      </td>

      <td style={{ textAlign: "left" }}>
        Admin is now internally alerted to CSV upload failures.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1224
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed an issue with searching contacts when making a new contact list from existing contacts.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1249
      </td>

      <td style={{ textAlign: "left" }}>
        Changed URL shortener to where only trusted accounts have access to that feature.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1223
      </td>

      <td style={{ textAlign: "left" }}>
        Added an alert when making an SMS campaign.  If the user applies a custom variable not previously defined in any of the contacts receiving the campaign.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1226
      </td>

      <td style={{ textAlign: "left" }}>
        Changed the wording when deleting a contact.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1232
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed an issue with the First Campaign upon signup.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1222
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed an issue where Canadian phone numbers couldn't be reached.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1218
      </td>

      <td style={{ textAlign: "left" }}>
        With the new limitations on non-company emails for signup, the signup page will now highlight errors appropriately.
      </td>
    </tr>
  </tbody>
</Table>
