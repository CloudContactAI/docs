---
title: Ruby
excerpt: Send SMS or MMS with Ruby
deprecated: false
hidden: false
metadata:
  title: Send emails, SMS, and MMS with Ruby - CloudContactAI
  description: >-
    Learn how to send your first email, SMS, and MMS using the CloudContactAI
    Ruby SDK
  image: >-
    https://files.readme.io/98fd17d59b6565ca03710a2f5873caf99b41db37aa9721ba341cd3b783f6706a-Group_14.png
  keywords:
    - email
    - mms
    - sms
    - ruby
    - api
  robots: index
---
Learn how to send your first SMS or MMS using the CCAI Ruby SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Paid Plan
* Create an API Key
* Get your Client ID
* Watch this video if you need help
* <Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />
  <br />

## 1. Install

Get the CCAI Ruby SDK.

**Requirements:** Ruby 2.6 or higher

```text
gem install ccai
```

Or add your Gemfile:

```ruby
gem 'ccai'
```

<br />

## 2. Send SMS message

```ruby
require 'ccai'

# Initialize the client
client = CCAI.new(
  client_id: 'YOUR-CLIENT-ID',
  api_key: 'YOUR-API-KEY'
)

# Send a single SMS
response = client.sms.send_single(
  'John',
  'Doe',
  '+15551234567',
  'Hello ${firstName}, this is a test message!',
  'Test Campaign'
)

puts "Message sent with ID: #{response.id}"

# Send to multiple recipients
accounts = [
  CCAI::SMS::Account.new(
    first_name: 'John',
    last_name: 'Doe',
    phone: '+15551234567'
  ),
  CCAI::SMS::Account.new(
    first_name: 'Jane',
    last_name: 'Smith',
    phone: '+15559876543'
  )
]

campaign_response = client.sms.send(
  accounts,
  'Hello ${firstName} ${lastName}, this is a test message!',
  'Bulk Test Campaign'
)

puts "Campaign sent with ID: #{campaign_response.campaign_id}"
```

<br />

## 3. Send MMS message

```ruby
require 'ccai'

# Initialize the client
client = CCAI.new(
  client_id: 'YOUR-CLIENT-ID',
  api_key: 'YOUR-API-KEY'
)

# Define progress tracking
options = CCAI::SMS::Options.new(
  timeout: 60,
  on_progress: ->(status) {
    puts "Progress: #{status}"
  }
)

# Complete MMS workflow (get URL, upload image, send MMS)
image_path = 'path/to/your/image.jpg'
content_type = 'image/jpeg'

# Define recipient
account = CCAI::SMS::Account.new(
  first_name: 'John',
  last_name: 'Doe',
  phone: '+15551234567'  # Use E.164 format
)

# Send MMS with image in one step
response = client.mms.send_with_image(
  image_path,
  content_type,
  [account],
  'Hello ${firstName}, check out this image!',
  'MMS Campaign Example',
  options
)

puts "MMS sent! Campaign ID: #{response.campaign_id}"
```

## 4. Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-ruby).