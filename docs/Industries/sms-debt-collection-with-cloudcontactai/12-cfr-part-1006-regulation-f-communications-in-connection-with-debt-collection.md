---
title: >-
  Communications in connection with debt collection - 12 CFR Part 1006
  (Regulation F) -
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
CloudContactAI by default provides checks to ensure thatc ontacts aren't contacted outside of 8:00 am and 9 pm, local time at the contact's location.

A link to the CFPB inconvenient timezone rule is here

[https://www.consumerfinance.gov/rules-policy/regulations/1006/6/#de38a82277268f404065254dafd5d4914192d0c3b36d54d4642f206f](https://www.consumerfinance.gov/rules-policy/regulations/1006/6/#de38a82277268f404065254dafd5d4914192d0c3b36d54d4642f206f)

The inconvenient timezone rule is defined as

(b) Communications with a consumer—

(1) Prohibitions regarding unusual or inconvenient times or places. Except as provided in paragraph (b)(4) of this section, a debt collector must not communicate or attempt to communicate with a consumer in connection with the collection of any debt:

(i) At any unusual time, or at a time that the debt collector knows or should know is inconvenient to the consumer. In the absence of the debt collector’s knowledge of circumstances to the contrary, a time before 8:00 a.m. and after 9:00 p.m. local time at the consumer’s location is inconvenient; or

CloudContactAI by uses the area code of phone number 1 that is provided by the Contact to ascertain whether an SMS, manual voice dial, or email can be sent to the Contact at the time of the message. The implementation of the inconvenient timezone rule looks up the contact's area code to determine their current local time and applies that offset to see whether a message, email, or call can be sent.

The inconvenient timezone rule can be enabled or disabled on the Settings\\TCPA Compliance tab.

![](https://files.readme.io/23966ee-image.png)
