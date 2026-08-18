---
title: AI Agents
excerpt: >-
  Build intelligent, automated SMS and Email agents that respond to customer messages in real time using AI.
deprecated: false
hidden: false
metadata:
  title: AI Agents with CloudContactAI
  description: >-
    CloudContactAI AI Agents use OpenAI, DSPy, and FAISS to automatically respond to inbound SMS messages with context-aware, accurate replies.
  image: >-
    https://files.readme.io/9c34fc90e99b3fe9134e34cb047572df42d878e2ece3792045dd887707fca2f8-CCAI_800x800.png
  keywords:
    - ai agents
    - sms
    - email
    - automation
    - inbound
    - chatbot
    - cloudcontactai
  robots: index
next:
  pages:
    - type: basic
      slug: how-to-configure-your-cloudcontactai-agent
      title: How to configure your CloudContactAI Agent
---

CloudContactAI AI Agents automatically respond to inbound SMS and Email messages using your own knowledge base and AI-powered language models. Instead of manually replying to every customer message, you configure an agent once and it handles responses at scale — accurately and in context.

## How It Works

AI Agents are built on three core technologies:

| Component | Role |
| --- | --- |
| **[OpenAI](https://openai.com)** | Understands customer messages and generates human-like responses |
| **[DSPy](https://dspy-docs.vercel.app/intro/)** | Orchestrates the interaction between OpenAI and your knowledge base |
| **[FAISS](https://ai.meta.com/tools/faiss/)** | Retrieves relevant information from your knowledge base to ground responses in your data |

**The flow for every inbound message:**

1. Customer sends an SMS or Email to your CCAI number or address
2. FAISS searches your knowledge base for relevant context
3. OpenAI generates a response using that context
4. CCAI delivers the response back to the customer automatically

## Benefits

- **Instant responses** — customers get answers immediately, any time of day
- **Context-aware** — responses are grounded in your specific knowledge base, not generic AI output
- **Scalable** — handles high message volumes without additional staff
- **Customizable** — configure agent personality, tone, and behavior per phone number or use case

---

## Setup

<Steps>

<Step title="Create an AI Agent">

Navigate to **Agents** in the left sidebar. You'll see separate tabs for SMS and Email agents — both start empty.

<Image align="center" src="https://files.readme.io/950b37c6b96e0f53f68e23c6b71d0c9bca02ab1b6540b07b2c71ad31fcec3c35-Screenshot_2024-12-19_111615.png" />

Click **Create AI Agent**. Give your agent a name and a description that defines how it should behave. Include any relevant information — product details, FAQs, links — that the agent should use when responding.

<Image align="center" src="https://files.readme.io/b96fb3ac2469299adbc46617828721dfe256bbb0df658006b134b65509df4ee0-Screenshot_2024-12-19_111632.png" />

You can edit the agent name, update its parameters, or delete it at any time.

<Image align="center" src="https://files.readme.io/734bb2ff0ec76ddbe1cdf38c1609e4c35bd7d89bc79b9c67aceb023f124f6695-Screenshot_2024-12-19_112546.png" />

</Step>

<Step title="Enable the AI Agent on a phone number">

Go to **Settings → General Settings**. At the bottom of the page you'll find the AI chatbot toggle. Enable it to activate the agent.

<Image align="center" src="https://files.readme.io/25a9cd02024063d94986d78e0690be91e9bef229261d93a915d0e5e857d709aa-Screenshot_2024-12-19_114454.png" />

Enabling the toggle opens a dropdown of available agent personalities — choose a built-in option or select **Custom Agent** to use one you created.

<Image align="center" src="https://files.readme.io/98920213f07250a3d911d73b8bbc551e54c78e0dc9c9608d934fe50bbeb417a2-Screenshot_2024-12-19_111702.png" />

</Step>

<Step title="Select your agent">

If you select **Custom Agent**, a second dropdown appears listing your created agents. If you haven't built one yet, you'll see a prompt to create one.

<Image align="center" src="https://files.readme.io/994bff40173438e2895f38dd6255563f06c348cb72c3cd4158c5f9dbee19e612-Screenshot_2024-12-19_112616.png" />

</Step>

<Step title="Save and go live">

Click **Save**. The agent is now active on your account and will automatically respond to inbound messages.

<Image align="center" src="https://files.readme.io/9978c825b73e41a4caac76c7ed2e00cb49ed4abebf6d67f12f8fafd5a1a169a9-Screenshot_2024-12-19_112904.png" />

To disable the agent at any time, return to **Settings → General Settings** and toggle it off.

</Step>

</Steps>

---

## Next Steps

<Cards columns={2}>
  <Card title="Configure Your Agent" href="/docs/how-to-configure-your-cloudcontactai-agent" icon="fa-duotone fa-robot" description="Fine-tune your agent's behavior, tone, and knowledge base." />
  <Card title="SMS Workflows" href="/docs/flows" icon="fa-duotone fa-diagram-project" description="Combine AI Agents with automated workflows for full conversation automation." />
</Cards>