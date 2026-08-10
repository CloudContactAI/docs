---
title: (07-16-25) Release Notes
deprecated: false
hidden: false
metadata:
  robots: index
---
| Jira Ticket | Description                                                                                                                                                                                       |
| :---------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CLOUD-2268  | Now the callbacks for incoming and out messages will work as intended.                                                                                                                            |
| CLOUD-2277  | Other non-visible things like we move the config for the questionnaires and the answers for subscriptions out of Mongo into Postgres.                                                             |
| CLOUD-2270  | Put up the config for a default message for all the incoming messages that is only sent if there is no other key matching the user message and if the message is an opt-out message, like 'stop'. |
| CLOUD-2111  | Opt-out messages like a stop will now mark the contact as do not text, likewise opt-in messages like a start will remove the do not text mark from that contact.                                  |
| CLOUD-2266  | Send messages screen will now have tabs for sent, all, error, and pending messages.                                                                                                               |
| CLOUD-2294  | Trial accounts now can use API keys and their limit can be configure from the account details on the Admin and also their trial date can be configure from the Admin.                             |