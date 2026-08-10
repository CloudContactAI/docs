---
title: 'Reducing Inbox Noise: Using Amazon Nova Pro to Automate SMS Compliance'
deprecated: false
hidden: false
metadata:
  description: >-
    As a developer, there is nothing more frustrating than building a high-scale
    messaging platform only to have the "human" inbox flooded with
    machine-generated noise. When you’re managing thousands of outbound SMS
    campaigns, the inbound responses often include automated "line not
    monitored" alerts, emergency redirects, or system opt-in confirmations.
  image: >-
    https://files.readme.io/7d99852e870fb64eed1e933b075a52e2dbc1af7efbed0017865e2041c4f628d9-ai-prompt-do-not-contact-ccai.png
  robots: index
---
<br />

As a developer, there is nothing more frustrating than building a high-scale messaging platform only to have the "human" inbox flooded with machine-generated noise. When you’re managing thousands of outbound SMS campaigns, the inbound responses often include automated "line not monitored" alerts, emergency redirects, or system opt-in confirmations.

At **CloudContactAI**, we faced a classic "needle in a haystack" problem: our users were manually reviewing hundreds of messages just to find the one or two that actually required a human response.

To solve this, we leveraged **Amazon Nova Pro** to build an intelligent, GenAI-powered filtering layer. Here’s how we did it.

***

<Image align="center" border={false} src="https://files.readme.io/4ead0270e7f0625969b1717f6fa0016da2a0dd5f6ddd8ddfaa07da9a2f9ba72f-ai-prompt-do-not-contact-ccai.png" />

### The Architecture of a Smart Filter

The goal was simple: pass every inbound SMS through an AI model to determine if the sender is a human or a machine, then take immediate action in the CRM.

#### 1. The Prompt Engineering

The core of this functionality lies in a strictly constrained prompt. To ensure the output is programmatically actionable, we require a boolean response without any prose.

**The System Prompt:**

> _"This is a text message received by SMS. Validate if this message comes from a bot, a machine, or any automated response system or not. Just answer true or false. Do not explain the reason."_

#### 2. Evaluating the Data

We tested the model against common "dead-end" responses that typically clutter an inbox:

* **System Alerts:** _"This line is not monitored for messages. Please call 229-391-4100..."_
* **Emergency Redirects:** _"If this is an emergency, please call 911."_
* **Carrier Notifications:** _"You are now opted-in. To opt out, reply STOP."_

By feeding these into **Amazon Nova Pro**, the model accurately returns `True` for automated responses, allowing our backend to trigger automated workflows.

***

### Automating the Workflow: Actions & Archiving

Detecting the noise is only half the battle; the second half is cleaning it up. We integrated specific actions into our production environment based on the AI’s evaluation:

1. **Mark as "Do Not Contact" (DNC):** If the response is `True` (Machine), the contact is flagged to prevent future wasted spend and compliance issues.
2. **Archive Chat:** The message is immediately moved from the active inbox to an archived folder.

#### The Logic Flow:

```javascript
// Example logic for processing the Nova Pro output
const messageAnalysis = await getAmazonNovaProResponse(inboundSMS);

if (messageAnalysis.toLowerCase().includes("true")) {
    // Action: Flag as DNC and clean up the UI
    markContactAsDoNotContact(contactID);
    archiveChatFromInbox(chatID);
    console.log("Automated response detected. Contact flagged and archived.");
} else {
    // Action: Leave in inbox for human engagement
    notifyAgent(chatID);
}
```