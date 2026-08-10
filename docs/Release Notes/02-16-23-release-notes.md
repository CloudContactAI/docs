---
title: (02-16-23) Release Notes
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: 'CloudContactAI release 02/16/23: Auto-response for inbound SMS, pagination improvements, payment fix.'
  robots: index
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
        CLOUD-1180
      </td>

      <td style={{ textAlign: "left" }}>
        Creating a contact list from existing contacts will now retain the contacts' phone numbers.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1179
      </td>

      <td style={{ textAlign: "left" }}>
        When manually adding contacts to a list, contacts will now properly paginate at 10 contacts instead of 9.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1163
      </td>

      <td style={{ textAlign: "left" }}>
        Resolved issues with payments not cancelling if a first payment attempt fails and a second/subsequent one clears.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1167
      </td>

      <td style={{ textAlign: "left" }}>
        Added timestamps to admin view as to when an account was made.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1174
      </td>

      <td style={{ textAlign: "left" }}>
        Added last/first page buttons to pagination.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1166
      </td>

      <td style={{ textAlign: "left" }}>
        Added alerts for admin when people make a purchase.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1115
      </td>

      <td style={{ textAlign: "left" }}>
        Added option to phone numbers where all inbound SMS get the same response.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1175
      </td>

      <td style={{ textAlign: "left" }}>
        Added a 'to' and 'from' number to the view campaign results tab.
      </td>
    </tr>
  </tbody>
</Table>
