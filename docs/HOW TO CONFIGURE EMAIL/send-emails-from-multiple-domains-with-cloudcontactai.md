---
title: Send Emails from Multiple Domains with CloudContactAI
excerpt: >-
  The recent Gmail and Yahoo Inbox sender requirements have made it so you don't
  want to send outbound emails through your corporate domain.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
When sending emails through CloudContactAI, we recommend that you provision multiple new domains. For each domain, we'll establish two mailboxes. We'll then ramp up emails slowly to prevent your domain being flagged for Spam under the recent [Gmail and Yahoo Mail sender requirements](https://cloudcontactai.com/gmail-yahoo-mail-new-email-sender-requirements/).

1. Provision multiple domains from your favorite domain registrar. We recommend [CloudFlare](https://cloudflare.com), [GoDaddy](https://godaddy.com), [AWS Route 53](https://aws.amazon.com/route53/), or [Google Domains](https://domains.google.com) . If your domain is example.org, then we'd recommend provisioning example.ai, example.org, example.net as domains that we'd send emails from.
2. Next, for these purchased domains, we prefer to use CloudFlare as the name server for the domains. To make use of CloudFlare, you first need to sign up for a free acount, and then you need to update the name servers of your domains to use [CloudFlare's name servers](https://developers.cloudflare.com/dns/zone-setups/full-setup/setup/). CloudFlare has the following benefits: 
   1. They provides SSL certificates for free. 
   2. They make domains easy to manage. 
   3. Through Cloudflare, we can easily put in a redirect rule to point your new domain, e.g. example.org, to your old domain, example.com. 
   4. We can manage your Email Deliverability in CloudFlare 
3. After we've setup your domain with CloudFlare, then we'll login to CloudContactAI.
4. On the Settings\\Email Config tab, you'll have the option of picking SendGrid or AWS SES. We prefer AWS SES.
5. Next, you'll need to put in the recently purchased domains and specify the email inboxes. Please work with the CloudContactAI Support team to configure SES. If you're familiar with AWS, you can try to follow these steps [here](https://developer.cloudcontactai.com/docs/aws-simple-email-system-how-to-setup-integration)\
   ![](https://files.readme.io/be3482743ea2d498fdece9b920b8200c7da5b2c93c05c55f2eabc9195caf2345-image.png)
6. After your Settings\\Email Config tab have been configured properly, CloudContactAI will add SNS topics and Webhooks to track bounces, complaints, unsubscribes, and opens. 
7. Navigate to the Email Campaigns section to start your outbound email campaigns!
