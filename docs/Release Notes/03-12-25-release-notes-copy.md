---
title: (03-12-25) Release Notes (COPY)
deprecated: false
hidden: false
metadata:
  robots: index
---
| Jira Ticket | Description                                                                                                                                                         |
| :---------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CLOUD-2025  | Updated the campaign split count and improved data throughput for downloading large campaign results.                                                               |
| CLOUD-2071  | A lot of data is now on campaign\_messages table.  To avoid it, the email text will be empty.  The message preview use the contact data and render it in client UI. |
| CLOUD-2060  | Messages queries are excluded and now use the same mechanics of the regular messages.                                                                               |
| CLOUD-2051  | Added replica database to emails.                                                                                                                                   |
| CLOUD-2028  | Made fixes to the email dashboard displaying incorrect information.                                                                                                 |