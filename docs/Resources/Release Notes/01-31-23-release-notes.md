---
title: (01-31-23) Release Notes
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: 'CloudContactAI release 01/31/23: Onboarding wizard, subscription cancellation fix, CSV upload fix.'
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
        CLOUD-1118
      </td>

      <td style={{ textAlign: "left" }}>
        Introduced an onboarding wizard.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1143
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed an issue where automated email messages couldn't be removed in the admin panel.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1149
      </td>

      <td style={{ textAlign: "left" }}>
        Ensured the industry dropdown in the SMS campaign creator would only populate with industries that had templates for them.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1131
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed an issue regarding spontaneous cancelling of a subscription plan.  Also added a verification email with a cancelled plan.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        CLOUD-1146
      </td>

      <td style={{ textAlign: "left" }}>
        Fixed an issue where uploading a CVS during a campaign would create a contact list that wouldn't populate.
      </td>
    </tr>
  </tbody>
</Table>
