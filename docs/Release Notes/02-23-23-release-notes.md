---
title: (02-23-23) Release Notes
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
        CLOUD-1184
      </td>

      <td style={{ textAlign: "left" }}>
        Added admin accounts tab to admin view.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1186
      </td>

      <td style={{ textAlign: "left" }}>
        Resolved issue with admin invite regarding the invite emails.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1117
      </td>

      <td style={{ textAlign: "left" }}>
        Added 'date added' and 'date updated' fields to contacts.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1142
      </td>

      <td style={{ textAlign: "left" }}>
        Changed it where after someone has deleted all contacts in the contacts tab, the table is now replaced with the 'no contacts' splash screen.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1177
      </td>

      <td style={{ textAlign: "left" }}>
        Updated logic for the admin confirmation splash screen that untrusted users will receive while trusted users will not get this verification splash screen when sending a campaign.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1173
      </td>

      <td style={{ textAlign: "left" }}>
        Deleting contacts will no longer break the listed messages on the Sent tab.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1182
      </td>

      <td style={{ textAlign: "left" }}>
        Implemented autofill variables for debt collection.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1185
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed an vulnerability where users could circumnavigate the email verification process by abusing the "forgot password" button.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1176
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed issue where messages sent to out-of-country contacts that would throw an error due to in-country limits would still read as 'sent' in the Sent tab.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1168
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed issue where the error that would be thrown when sending an out-of-country message would work inconsistently.  Ties into CLOUD-1176.
      </td>
    </tr>
  </tbody>
</Table>
