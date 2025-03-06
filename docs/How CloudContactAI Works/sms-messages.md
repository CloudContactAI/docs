---
title: SMS Messages Details
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
One SMS message is limited to 160 characters, which we count as one message segment.

## What is an message segment?

Messages that are longer than 160 characters are divided into groups of messages of 160 characters each. If you send a message with 310 characters, this would count as 2 message segments, as it will take two 160 character messages to transmit.

If you include unicode characters or any special characters like emoji or new lines in your message, this requires us to send additional data with each message so cell phones can render them properly.
