---
title: 'Amazon SES: How to Setup Integration with the Simple Email Service (SES)'
excerpt: ''
deprecated: false
hidden: false
metadata:
  description: >-
    Setup your CloudContactAI account to send emails with Amazon Simple Email
    Services (SES)
  image: >-
    https://files.readme.io/3a0b39a3a80e3732c2f8f6c13d03a367fb2304294426addbb3e1434e6932fa85-Group_84_1.png
  keywords:
    - amazon SES
    - email
    - api
    - cloudcontactai
  robots: index
next:
  description: ''
---
<Embed url="https://www.youtube.com/watch?v=yA3PTtwJF1s" title="Setting up CloudContactAI with Amazon SES" favicon="https://www.google.com/favicon.ico" image="https://i.ytimg.com/vi/yA3PTtwJF1s/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/watch?v=yA3PTtwJF1s" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FyA3PTtwJF1s%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DyA3PTtwJF1s%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FyA3PTtwJF1s%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

<br />

In order to send outbound emails with CloudContactAI, CCAI must be integrated with a third-party email management system.  This tutorial will walk you through the steps of configuring Amazon Simple Email Service (SES).

<Image align="center" src="https://files.readme.io/6996423f6cf4e1e59bc5739ef754a1fd6516e59ca4b0b5451eb396aa03c4904a-ccai_email_provider_options.png" />

1. Upon selecting Amazon SES, CloudContactAI will prompt the user for email that you'd like to send emails through, the AWS region the account is sending from, an IAM access key, and the corresponding secret key.

<Image align="center" src="https://files.readme.io/8e08b40478270e48460b6d59e35e0dafb01b5918755541678691fa3ed48b903d-ccai_ses_credential_requirements.png" />

2. Most likely, you won't have any of the above information, which means you'll need to login to an AWS account to provision as IAM user with keys and permissions to send emails and create SNS topics.  Login to your AWS account, or have a CCAI Support Agent do this for you. Provision a new IAM user. For clarification, this needs to be done under IAM, not the IAM Identity Center.

<Image align="center" src="https://files.readme.io/64a8b3add9247beac3366aed1569f756afaba94757fa724843eec9a0977728a4-aws_iam_users.png" />

<Image align="center" src="https://files.readme.io/9c06a8c129a06d94b7b96bfbd47dfc26b4e47ffca8c76ec6c66ae2d0b29242ce-aws_new_iam_user.png" />

Building a new IAM user is straightforward.  The important step is establishing the correct permissions to  the IAM user.  The following permissions needs to be associated to the user, AmazonSNSFullAccess and AmazonSESFullAccess.  Forgetting either will cause an error if the user attempts to connect via CCAI.  In the example below, we'll add a user to a group, and the permissions to the group. 

<Image align="center" src="https://files.readme.io/794e88034efa8246ce6b6ba8f5c0b3f1c7872c6a586f6e0beb028f73789dc58e-aws_iam_add_group.png" />

<Image align="center" src="https://files.readme.io/9f089f5d9f3596c738b3177b4f9de7f2be1d67fbec438454ec9cb50c248c4563-aws_iam_sns_full_access.png" />

3. The user will still need to add an access key. Drill into the new user from the user menu and select "create access key" at the top right.  For the CCAI email use case, it's preferable to toggle "other" for the use-case and best-practices options.  For convenience's sake, the user can either download the key as a CSV file or copy/paste the keys into a text file.  In either case, these files should be carefully handled.

<Image align="center" src="https://files.readme.io/aeeac581a9e49c84fc1f10ce01f6538e4e86344b64c6ed0118030ee226917fef-aws_create_access_key_other.png" />

<Image align="center" src="https://files.readme.io/398076889f2e0a8a77ac8f82bd4b0de8aa0a04525463d87c37699b8c04e85d37-aws_access_key_done.png" />

4. Then the user will need to generate an email to send from and a profile for the domain they are using if they are using a unique email address.  The option for generating a new email identity can be found under the "identities" tab on Amazon SES.  AWS will then send the chosen email with a link to verify the address.

<Image align="center" src="https://files.readme.io/05873451a8e68805006a816bd34165657c5f5b766f060c89747527cef8e677f4-aws_ses.png" />

<Image align="center" src="https://files.readme.io/c662476b4c5122a1bbe264d08f7331bc3e95c431ce40fbd8337f06a2b3f1a676-aws_ses_create_identity.png" />

<Image align="center" src="https://files.readme.io/bf6634a4236eb60c80317bbe6f2ebe303a95be36b00fd65de63686433375ee65-aws_ses_email_verified.png" />

5. Verifying a domain is a considerably more complicated process.  AWS requires the user to upload the Domain Name System (DNS) records and methods of verification will differ based on the DomainKeys Identified Mail (DKIM) authentication option used.  For more in-depth details about the steps needed to establish a domain, verify a domain, and troubleshoot domain verification, refer to the official [AWS documentation](https://docs.aws.amazon.com/ses/latest/dg/creating-identities.html).

<Image align="center" src="https://files.readme.io/e309272753c0bc629a3e0a79a20495684324491bf1e7e22ad36c4bd272969aa7-aws_ses_domain.png" />

6. Finally, there is the AWS region.  The dropdown at the top-left of the screen will show the account's selected AWS region.  If an email has already been established, it must be properly migrated if the region is changed.

<Image align="center" src="https://files.readme.io/d8e4fc5585be080d46c97e45b70e591a58b8b6e8c84a4bf343911d6ad730a466-aws_region.png" />

7. Insert the appropriate credentials into their respective boxes on CCAI and the CCAI account will be ready to use the email feature.

<Image align="center" src="https://files.readme.io/2a7f98e590a8af7342e29b8e4493a9a08b4b5e5d6fe3b03bb8561e242e361519-ccai_aws_ses_successful_format.png" />

8. When you hit the Update button, CloudContactAI will go into your AWS account to create the configuration sets, topics, and event callback links. You'll see the following screen.
9. ![](https://files.readme.io/74b183056536b81f548bb47cea1a5f6624f97cce6c8f6cc0370420fdde77ac7b-image.png)

   Underneath the covers, in your AWS, CloudContactAI creates the AWS SES Configuration set for you.
10. ![](https://files.readme.io/a795b7679099aa29843202fa47c377fba3ea09fb00f01d3b9a87daccfa4d18e1-image.png)

    CloudContactAI will configure the Event destinations for you to handle Hard bounces, Complaints, and Deliveries
11. ![](https://files.readme.io/c8f7b4e1191ca9e7cfdadbea99b4f99c929e3994d73817708f5409d86c3b1ce8-image.png)

    The Email Events will make use of an AWS SNS Topic
12. ![](https://files.readme.io/a4a40bed9bc5664ed0e765c1946508c3a9d96005b666c8c75e41a6acd2e5c778-image.png)

    The AWS SNS Topic will route these events back to a CloudContactAI endpoint to update your Contacts in CCAI.
13. ![](https://files.readme.io/7e123371b4e7ef27036a38b53c312a5d56663de061d68290a334b5d5c59ed436-image.png)

    You should be good to go!