---
title: Webhooks
deprecated: false
hidden: true
metadata:
  robots: index
---
> Use webhooks to notify your application about SMS and email events.

## What is a webhook?

CloudContactAI uses webhooks to push real-time notifications to you about your SMS and email sending. All webhooks use HTTPS and deliver a JSON payload that can be used by your application. You can use webhook feeds to do things like:

* Receive SMS delivery notifications
* Receive incoming SMS messages
* Automatically remove bounced email addresses from mailing lists
* Create alerts in your messaging or incident tools based on event types
* Store all send events in your own database for custom reporting/retention

## Steps to receive webhooks

You can start receiving real-time events in your app using the steps:

1. Create a local endpoint to receive requests
2. Register your development webhook endpoint
3. Test that your webhook endpoint is working properly
4. Deploy your webhook endpoint to production
5. Register your production webhook endpoint

## 1) Create a local endpoint to receive requests

In your local application, create a new route that can accept POST requests.

For example, you can add an API route on Next.js:

```js pages/api/webhooks.ts
import type { NextApiRequest, NextApiResponse } from 'next';

export default (req: NextApiRequest, res: NextApiResponse) => {
  if (req.method === 'POST') {
    const payload = req.body;
    console.log(payload);
    res.status(200);
  }
};
```

On receiving an event, you should respond with an `HTTP 200 OK` to signal to CloudContactAI that the event was successfully delivered.

## 2. Register your development webhook endpoint

Register your publicly accessible HTTPS URL in the CloudContactAI dashboard.

You can create a tunnel to your localhost server using a tool like\
[ngrok](https://ngrok.com/download). For example:
`https://8733-191-204-177-89.sa.ngrok.io/api/webhooks`

Using ngrok will allow you to create a secure tunnel from the internet to your local machine and provide a public HTTPS URL for webhook testing

<br />

## 3. Test that your webhook endpoint is working properly

Send a few test emails to check that your webhook endpoint is receiving the events.

<img alt="Webhook Events List" src="https://mintlify.s3.us-west-1.amazonaws.com/cloudcontactai/images/dashboard-webhook-events-list.png" />

## 4. Deploy your webhook endpoint

After you're done testing, deploy your webhook endpoint to production.

## 5. Register your production webhook endpoint

Once your webhook endpoint is deployed to production, you can register it in the CloudContactAI dashboard.

## FAQ

### What is the retry schedule?

If CloudContactAI does not receive a 200 response from a webhook server, we will retry the webhooks.

Each message is attempted based on the following schedule, where each period is started following the failure of the preceding attempt:

* 5 seconds
* 5 minutes
* 30 minutes
* 2 hours
* 5 hours
* 10 hours

### What happens after all the retries fail?

After the conclusion of the above attempts the message will be marked as failed, and you will get a webhook of type `message.attempt.exhausted` notifying you of this error.

### What IPs do webhooks POST from?

If your server requires an allowlist, our webhooks come from the following IP addresses:

* `44.228.126.217`
* `50.112.21.217`
* `52.24.126.164`
* `54.148.139.208`
* `2600:1f24:64:8000::/52`

## Try it yourself

<Card title="Webhook Code Example" icon="arrow-up-right-from-square" href="https://github.com/cloudcontactai/resend-examples/tree/main/with-webhooks">
  See an example of how to receive webhooks events for CloudContactAI emails.
</Card>