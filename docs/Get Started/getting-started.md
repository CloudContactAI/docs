---
title: Quickstart with CloudContactAI
excerpt: >-
  Get up and running with CloudContactAI in minutes. Send your first SMS or Email using the dashboard or API.
deprecated: false
hidden: false
metadata:
  title: Quickstart with CloudContactAI
  description: >-
    Get up and running with CloudContactAI in minutes. Send your first SMS or Email using the dashboard or API.
  image: >-
    https://files.readme.io/25f246c82ca730ffcb9b35c64323e936119d314ca4dacf7031b43ed912c72333-Group_14.png
  keywords:
    - email
    - sms
    - api
    - quickstart
    - cloudcontactai
  robots: index
---

CloudContactAI is ready to use the moment your account is created. This guide walks you through signing up, getting oriented in the dashboard, and sending your first message.

## Prerequisites

- A business email address, Gmail account, or Amazon account to sign up with
- A phone number or verified email domain to send from (see [Acquire a Phone Number](/docs/phone-numbers) and [Configure Email Domain](/docs/configure-email-domain))

## Steps

<Steps>

<Step title="Create your account">

Go to [cloudcontactai.com](https://cloudcontactai.com) and click **Sign Up**. Enter your business email and name, then click **Create Account**.

![Sign up screen](https://files.readme.io/cf6d6fc-Screenshot_2022-09-13_101600.png)

You'll receive a verification email. Click the link to verify your address, then set your password.

![Verification screen](https://files.readme.io/bdafce4-Screenshot_2022-09-13_102503.png)

</Step>

<Step title="Get oriented in the dashboard">

After logging in you'll land on the CloudContactAI dashboard. From here you can manage contacts, run campaigns, configure phone numbers, and access all settings.

![Dashboard](https://files.readme.io/a6bdddf-Screen_Shot_2023-03-21_at_2.14.37_PM.png)

</Step>

<Step title="Get your API Key">

Navigate to **Account → Settings** to find your **Client ID** and create an **API Key**. You'll need both to use the SDK or REST API.

See [Create API Key](/docs/quickstart-with-api) for a full walkthrough.

</Step>

<Step title="Send your first message">

Choose how you want to send:

<Cards columns={2}>
  <Card title="Send via SDK" href="/docs/nodejs" icon="fa-duotone fa-code" description="Use one of our SDKs to send SMS or Email programmatically." />
  <Card title="Send via Dashboard" href="https://app.cloudcontactai.com" icon="fa-duotone fa-browser" description="Send a campaign directly from the CloudContactAI dashboard." />
</Cards>

</Step>

</Steps>

## Next Steps

<Cards columns={3}>
  <Card title="Acquire a Phone Number" href="/docs/phone-numbers" icon="fa-duotone fa-phone" />
  <Card title="Configure Email Domain" href="/docs/configure-email-domain" icon="fa-duotone fa-envelope" />
  <Card title="Explore the API" href="/reference" icon="fa-duotone fa-code" />
</Cards>