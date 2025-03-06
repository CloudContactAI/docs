---
title: Quickstart with API
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Visual Guide

[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fwww.youtube.com%2Fembed%2FCXTrFkXnmXs%3Ffeature%3Doembed&display_name=YouTube&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DCXTrFkXnmXs&image=https%3A%2F%2Fi.ytimg.com%2Fvi%2FCXTrFkXnmXs%2Fhqdefault.jpg&key=7788cb384c9f4d5dbbdbeffd9fe4b92f&type=text%2Fhtml&schema=youtube\" width=\"854\" height=\"480\" scrolling=\"no\" title=\"YouTube embed\" frameborder=\"0\" allow=\"autoplay; fullscreen; encrypted-media; picture-in-picture;\" allowfullscreen=\"true\"></iframe>",
  "url": "https://www.youtube.com/watch?v=CXTrFkXnmXs",
  "title": "CloudContactAI API Tutorial",
  "favicon": "https://www.google.com/favicon.ico",
  "image": "https://i.ytimg.com/vi/CXTrFkXnmXs/hqdefault.jpg",
  "provider": "https://www.youtube.com/",
  "href": "https://www.youtube.com/watch?v=CXTrFkXnmXs",
  "typeOfEmbed": "youtube"
}
[/block]


<br />

## Account

Let's briefly go over using the API.  We will use an account with an Essentials Plan configuration for this demonstration.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8805053-getting_started_account.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


<br />

## Phone Number

Because this user has purchased a subscription, they have a phone number registered.  The A2P Brand and Campaign have been approved for (312) 638-0457.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fa66155-getting_started_phone.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


<br />

## Testing

Tests are supported through the following [API endpoint](https://developer.cloudcontactai.com/reference/creates-a-new-campaign-with-contacts).

For testing, you will need to get the ClientID and the API Key from your Settings tab as shown below.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5b1bf03-getting_started_api_key.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


<br />

The Client ID and API Key will be used in the REST API Request.  On the developer.cloudcontactai.com site, add the API Key to the Authorization prefixed with Bearer.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0a42408-getting_started_rest_api_request.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


You are required to specify the Client ID.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c3f04c2-getting_started_client_id.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


In the Body Params category, click Add Object.  You will need to specify the first name, last name, and phone number categories, or else the message will throw an error.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/afaf0c3-getting_started_required_categories.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


Outside of the account parameters, you will need a campaign name and message.  For example, we're giving the campaign the title of "First Campaign" and the message will read, “${firstName}, hello how’s it going?”

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e936871-getting_started_complete_campaign.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


The campaign has all the prerequisites and is ready to be sent.  Click on the "Try it!" button at the bottom of the Curl Request window.  The message will go out and the following will appear in the Response window.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/07a102d-getting_started_try_it_outcome.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


The message should appear both to the phone number the message was written for and under the "Sent" tab on the CCAI dashboard.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9691470-getting_started_text_message.png",
        "",
        ""
      ],
      "align": "center",
      "sizing": "200px"
    }
  ]
}
[/block]


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c1a8f47-getting_started_ccai_records.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


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