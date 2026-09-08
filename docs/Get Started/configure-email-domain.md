---
title: Configure Email Domain
excerpt: >-
  Step-by-step guide to configuring an email provider for outbound email in
  CloudContactAI. Supports Amazon SES and Twilio SendGrid.
deprecated: false
hidden: false
metadata:
  description: >-
    Set up your CloudContactAI account to send emails using Amazon SES or Twilio
    SendGrid.
  image: >-
    https://files.readme.io/3a0b39a3a80e3732c2f8f6c13d03a367fb2304294426addbb3e1434e6932fa85-Group_84_1.png
  keywords:
    - amazon SES
    - sendgrid
    - twilio
    - email
    - api
    - cloudcontactai
  robots: index
---
To send outbound emails with CloudContactAI, you need to connect a third-party email provider. CCAI supports two providers:

<Cards columns={2}>
  <Card title="Amazon SES" href="#amazon-ses" icon="fa-brands fa-aws" description="Best for teams already using AWS infrastructure." />
  <Card title="Twilio SendGrid" href="#twilio-sendgrid" icon="fa-duotone fa-envelope-open-text" description="Best for teams that want a dedicated email delivery platform." />
</Cards>

***

## Amazon SES

<Embed title="" typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=yA3PTtwJF1s" href="https://www.youtube.com/watch?v=yA3PTtwJF1s" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FyA3PTtwJF1s%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DyA3PTtwJF1s%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FyA3PTtwJF1s%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

### Prerequisites

- An AWS account with access to IAM and SES
- A verified email address or domain in Amazon SES

### SES Integration Steps

1\) Sign into your AWS Account. Be sure to set your account to the region you want to operate from using the dropdown in the upper right corner. Any previous services used on this AWS account that are setup fore the SES integration and are relevant to CCAI integration will need to be migrated to this new AWS region.

2\) Navigate to IAM > User > Create User.

3\) Add the user to a group with AmazonSNSFullAccess and AmazonSESFullAccess permissions enabled. If you haven't made a group already, you can make a new group in this same window using the Create Group button under User Groups. One final window will appear afterward to help validate all the correct configurations are implemented.

4\) After returning to the Users screen, drill into the freshly made user and navigate to Create Access Key in the Summary box.

5\) Select the "Other" radio button and click Next. Optional: add a tag for organizational purposes.

6\) Save the provided Access Key and Secret Access Key however is convenient.

7\) Navigate to Amazon SES > Identities > Create Identity. You will need to establish the email address you will be using on CCAI. After confirming the address, AWS will send that address a verification link. If the address uses a unique domain, a domain will also need to be established also through Create Identity.

8\) Return to CCAI and navigate to Email Campaign > Amazon SES. Provide all the relevant credentials in their respective categories and click Save.

<Steps>

<Step title="Select Amazon SES in CCAI">

In your CCAI account, navigate to **Settings → Email Config** and select **Amazon SES** as your provider. You'll be prompted for your sending email, AWS region, IAM access key, and secret key.

<Image align="center" src="https://files.readme.io/6996423f6cf4e1e59bc5739ef754a1fd6516e59ca4b0b5451eb396aa03c4904a-ccai_email_provider_options.png" />

<Image align="center" src="https://files.readme.io/8e08b40478270e48460b6d59e35e0dafb01b5918755541678691fa3ed48b903d-ccai_ses_credential_requirements.png" />

</Step>

<Step title="Create an IAM user in AWS">

Log into your AWS account and navigate to **IAM → Users**. Create a new IAM user (under IAM, not IAM Identity Center) and attach the following permissions:

- `AmazonSESFullAccess`
- `AmazonSNSFullAccess`

Both permissions are required — missing either will cause an error when connecting.

<Image align="center" src="https://files.readme.io/64a8b3add9247beac3366aed1569f756afaba94757fa724843eec9a0977728a4-aws_iam_users.png" />

<Image align="center" src="https://files.readme.io/794e88034efa8246ce6b6ba8f5c0b3f1c7872c6a586f6e0beb028f73789dc58e-aws_iam_add_group.png" />

<Image align="center" src="https://files.readme.io/9f089f5d9f3596c738b3177b4f9de7f2be1d67fbec438454ec9cb50c248c4563-aws_iam_sns_full_access.png" />

</Step>

<Step title="Generate an access key">

Drill into the new IAM user and click **Create access key**. Select **Other** for the use case. Save the access key and secret key — you'll need both for CCAI. Store them securely.

<Image align="center" src="https://files.readme.io/aeeac581a9e49c84fc1f10ce01f6538e4e86344b64c6ed0118030ee226917fef-aws_create_access_key_other.png" />

<Image align="center" src="https://files.readme.io/398076889f2e0a8a77ac8f82bd4b0de8aa0a04525463d87c37699b8c04e85d37-aws_access_key_done.png" />

</Step>

<Step title="Verify your sending identity in SES">

In AWS, navigate to **SES → Identities** and create an identity for the email address or domain you want to send from. AWS will send a verification email — click the link to confirm.

For domain verification, you'll need to add DNS records. See the [AWS SES documentation](https://docs.aws.amazon.com/ses/latest/dg/creating-identities.html) for full details.

<Image align="center" src="https://files.readme.io/05873451a8e68805006a816bd34165657c5f5b766f060c89747527cef8e677f4-aws_ses.png" />

<Image align="center" src="https://files.readme.io/bf6634a4236eb60c80317bbe6f2ebe303a95be36b00fd65de63686433375ee65-aws_ses_email_verified.png" />

</Step>

<Step title="Note your AWS region">

The AWS region dropdown is at the top-left of the AWS console. Make sure the region you use in CCAI matches the region where your SES identity is verified.

<Image align="center" src="https://files.readme.io/d8e4fc5585be080d46c97e45b70e591a58b8b6e8c84a4bf343911d6ad730a466-aws_region.png" />

</Step>

<Step title="Connect SES to CCAI">

Enter your credentials into CCAI and click **Update**. CCAI will automatically create the required AWS SES configuration sets, SNS topics, and event callback links in your AWS account.

<Image align="center" src="https://files.readme.io/2a7f98e590a8af7342e29b8e4493a9a08b4b5e5d6fe3b03bb8561e242e361519-ccai_aws_ses_successful_format.png" />

![](https://files.readme.io/74b183056536b81f548bb47cea1a5f6624f97cce6c8f6cc0370420fdde77ac7b-image.png)

CCAI configures bounce, complaint, and delivery event handling automatically. You're ready to send.

![](https://files.readme.io/7e123371b4e7ef27036a38b53c312a5d56663de061d68290a334b5d5c59ed436-image.png)

</Step>

</Steps>

***

## Twilio SendGrid

### Prerequisites

- A Twilio SendGrid account
- A verified sender identity or domain in SendGrid

<Steps>

<Step title="Select SendGrid in CCAI">

In your CCAI account, navigate to **Settings → Email Config** and select **Twilio SendGrid** as your provider.

</Step>

<Step title="Generate a SendGrid API key">

In your SendGrid account, go to **Settings → API Keys → Create API Key**. Grant it **Full Access** or at minimum **Mail Send** permissions. Copy the key — it will only be shown once.

</Step>

<Step title="Verify your sender identity">

In SendGrid, go to **Settings → Sender Authentication** and verify either a single sender email or a full domain. Domain authentication is recommended for production sending as it improves deliverability.

</Step>

<Step title="Connect SendGrid to CCAI">

Enter your SendGrid API key and verified sender email into CCAI and click **Update**. Your account is now ready to send email via SendGrid.

</Step>

</Steps>