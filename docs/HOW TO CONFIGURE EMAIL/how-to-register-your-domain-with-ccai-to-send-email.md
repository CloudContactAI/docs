---
title: How to Register Your Domain with CCAI to Send Email
excerpt: >-
  This guide will walk you through the process of registering a domain name and
  configuring it to send emails
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  keywords:
    - register your domain
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: send-emails-from-multiple-domains-with-cloudcontactai
      title: Send Emails from Multiple Domains with CloudContactAI
    - type: basic
      slug: aws-simple-email-system-how-to-setup-integration
      title: 'Amazon SES: How to Setup Integration with the Simple Email Service (SES)'
---
**Step 1:** Domain Registration

- Choose a Domain Registrar: Select a reputable domain registrar where you can register your domain name (e.g., [GoDaddy](https://godaddy.com), [Namecheap](https://namecheap.com), etc.).
- Search and Register: Search for your desired domain name availability and follow the registrar’s instructions to complete the registration process.
- Update Contact Information: Ensure that your contact information is up-to-date as per registrar requirements.

**Step 2**: Reach out to CloudContactAI Support so that we can configure your DNS records for you.  
We'll want you to grant delegate access to the DNS for your domain. 

You can learn how to do this here:

- Godaddy.com - [Grant Delegate Access](https://www.godaddy.com/help/invite-a-delegate-to-access-my-godaddy-account-12376)
- Namecheap.com - [Grant Delegate Access](https://www.namecheap.com/support/knowledgebase/article.aspx/192/46/how-do-i-share-access-to-my-domain-with-other-users/)
- CloudFlare.com - [Grant Delegate Access](https://chemicloud.com/kb/article/delegate-access-to-your-cloudflare-account/) 

**Step 3**: CloudContactAI Support will verify domain ownership and set up DNS records for your DKIM, SPF, and DMARC.  These records are required by the latest [Gmail and Yahoo Inbox sender requirements](https://cloudcontactai.com/gmail-yahoo-mail-new-email-sender-requirements/). 

**Step 4**:  CloudContactAI Support will test and validate your configuration for sending emails.

**Step 5**:  CloudContactAI Support will request sample emails from you to ensure that your emails adhere to our compliance guidelines. CloudContactAI will also request how often you send email. CloudContactAI will configure your recipients lists to manage bounces, complaints, and unsubscribe requests.

**Step 6**:  After CloudContactAI confirms that your email strategies adhere to our policies, CloudContactAI Support will remove you from our sandbox. You should be good to go