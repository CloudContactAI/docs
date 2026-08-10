---
title: Quickstart with API
excerpt: 'Get your API key and send your first campaign via the REST API.'
deprecated: false
hidden: false
metadata:
  title: QuickStart for using the CloudContactAI API
  description: >-
    Create your API Key and grab your Client ID to start using the
    CloudContactAI API in your code
  image: >-
    https://files.readme.io/89ad69052cb6620b245422b906035da9e855caa9c134ac674df60d0e01d8084f-Group_14.png
  keywords:
    - sms
    - email
    - mms
    - api
    - developer
  robots: index
next:
  description: ''
---
## Visual Guide

<Embed url="https://www.youtube.com/watch?v=CXTrFkXnmXs" title="CloudContactAI API Tutorial" favicon="https://www.google.com/favicon.ico" image="https://i.ytimg.com/vi/CXTrFkXnmXs/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

<br />

## Account

Let's briefly go over using the API.  We will use an account with an Essentials Plan configuration for this demonstration.

<Image align="center" src="https://files.readme.io/8805053-getting_started_account.png" />

<br />

## Phone Number

Because this user has purchased a subscription, they have a phone number registered.  The A2P Brand and Campaign have been approved for (312) 638-0457.

<Image align="center" src="https://files.readme.io/fa66155-getting_started_phone.png" />

<br />

## Testing

Tests are supported through the following [API endpoint](https://developer.cloudcontactai.com/reference/creates-a-new-campaign-with-contacts).

For testing, you will need to get the ClientID and the API Key from your Settings tab as shown below.

<Image align="center" src="https://files.readme.io/5b1bf03-getting_started_api_key.png" />

<br />

The Client ID and API Key will be used in the REST API Request.  On the developer.cloudcontactai.com site, add the API Key to the Authorization prefixed with Bearer.

<Image align="center" src="https://files.readme.io/0a42408-getting_started_rest_api_request.png" />

You are required to specify the Client ID.

<Image align="center" src="https://files.readme.io/c3f04c2-getting_started_client_id.png" />

In the Body Params category, click Add Object.  You will need to specify the first name, last name, and phone number categories, or else the message will throw an error.

<Image align="center" src="https://files.readme.io/afaf0c3-getting_started_required_categories.png" />

Outside of the account parameters, you will need a campaign name and message.  For example, we're giving the campaign the title of "First Campaign" and the message will read, “$\{firstName}, hello how’s it going?”

<Image align="center" src="https://files.readme.io/e936871-getting_started_complete_campaign.png" />

The campaign has all the prerequisites and is ready to be sent.  Click on the "Try it!" button at the bottom of the Curl Request window.  The message will go out and the following will appear in the Response window.

<Image align="center" src="https://files.readme.io/07a102d-getting_started_try_it_outcome.png" />

The message should appear both to the phone number the message was written for and under the "Sent" tab on the CCAI dashboard.

<Image align="center" width="200px" src="https://files.readme.io/9691470-getting_started_text_message.png" />

<Image align="center" src="https://files.readme.io/c1a8f47-getting_started_ccai_records.png" />

<br />

## Curl Request

If anything is confusing about the Curl Request window, here is an excerpt for reference.

```
curl --request POST \
     --url https://core.cloudcontactai.com/api/clients/YOUR-CLIENT-ID/campaigns/direct \
     --header 'Authorization: Bearer API-KEY-TOKEN' \
     --header 'accept: */*' \
     --header 'content-type: application/json' \
     --data '
{
  "accounts": [
    {
      "firstName": "Mike",
      "lastName": "Alvarez",
      "phone": "+17199411698"
    }
  ],
  "message": "Testing campaign setup with you, ${firstName} ${lastName}",
  "title": "Setup Validation Campaign"
}

```