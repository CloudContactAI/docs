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
<div style={{ margin: "16px 0 -8px 0" }}>
  <a
    href="https://app.cloudcontactai.com/register"
    style={{
      display: "inline-flex",
      alignItems: "center",
      justifyContent: "center",
      gap: "8px",
      backgroundColor: "#2563eb",
      color: "#ffffff",
      padding: "12px 20px",
      borderRadius: "12px",
      fontSize: "15px",
      fontWeight: 600,
      lineHeight: 1,
      textDecoration: "none",
      whiteSpace: "nowrap",
    }}
  >
    🔑 Get API Key
  </a>
</div>

Learn how to send your first SMS or MMS using the CCAI Ruby SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Trial Account [here](https://app.cloudcontactai.com/register)
* Get your Client ID from Account\Settings
* Create\Copy an API Key from Account Settings

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />

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

## 4. Step-by-Step MMS Workflow

```ruby
# Step 1: Get a signed URL for uploading
upload_response = client.mms.get_signed_upload_url(
  'image.jpg',
  'image/jpeg'
)

signed_url = upload_response.signed_s3_url
file_key = upload_response.file_key

# Step 2: Upload the image to the signed URL
upload_success = client.mms.upload_image_to_signed_url(
  signed_url,
  'path/to/your/image.jpg',
  'image/jpeg'
)

if upload_success
  # Step 3: Send the MMS with the uploaded image
  response = client.mms.send(
    file_key,
    accounts,
    'Hello ${firstName}, check out this image!',
    'MMS Campaign Example'
  )
  
  puts "MMS sent! Campaign ID: #{response.campaign_id}"
end
```

## 5. With Progress Tracking

```ruby
# Create options with progress tracking
options = CCAI::SMS::Options.new(
  timeout: 60,
  retries: 3,
  on_progress: ->(status) {
    puts "#{Time.now.strftime('%Y-%m-%d %H:%M:%S')} - #{status}"
  }
)

# Send SMS with progress tracking
response = client.sms.send(
  accounts,
  message,
  title,
  options
)
```

<br />

## 6. Send Email

```ruby
require 'ccai'

# Initialize the client
client = CCAI.new(
  client_id: 'YOUR-CLIENT-ID',
  api_key: 'YOUR-API-KEY'
)

# Send a single email
response = client.email.send_single(
  'John',
  'Doe',
  'john@example.com',
  'Welcome to Our Service',
  '<p>Hello John,</p><p>Thank you for signing up!</p>',
  'noreply@yourcompany.com',
  'support@yourcompany.com',
  'Your Company',
  'Welcome Email'
)

puts "Email sent with ID: #{response['id']}"

# Send email campaign to multiple recipients
campaign = {
  subject: 'Monthly Newsletter',
  title: 'July 2025 Newsletter',
  message: '<h1>Hello ${firstName},</h1><p>Here are our updates...</p>',
  senderEmail: 'newsletter@yourcompany.com',
  replyEmail: 'support@yourcompany.com',
  senderName: 'Your Company',
  accounts: [
    { firstName: 'John', lastName: 'Doe', email: 'john@example.com', phone: '' },
    { firstName: 'Jane', lastName: 'Smith', email: 'jane@example.com', phone: '' }
  ],
  campaignType: 'EMAIL',
  addToList: 'noList',
  contactInput: 'accounts',
  fromType: 'single',
  senders: []
}

response = client.email.send_campaign(campaign)
puts "Campaign sent with ID: #{response['campaignId']}"
```

## 7. Webhooks

```ruby
require 'ccai'

# Initialize the client
client = CCAI.new(
  client_id: 'YOUR-CLIENT-ID',
  api_key: 'YOUR-API-KEY'
)

# Register a webhook
config = {
  url: 'https://your-app.com/webhooks/ccai',
  events: [CCAI::Webhook::EventType::MESSAGE_SENT, CCAI::Webhook::EventType::MESSAGE_RECEIVED],
  secret: 'your-webhook-secret'
}

webhook = client.webhook.register(config)
puts "Webhook registered with ID: #{webhook['id']}"

# List all webhooks
webhooks = client.webhook.list
puts "Registered webhooks: #{webhooks.length}"

# Update a webhook
client.webhook.update(webhook['id'], { url: 'https://your-app.com/new-webhook' })

# Delete a webhook
client.webhook.delete(webhook['id'])

# Verify webhook signature (in your webhook handler)
signature = request.headers['X-CCAI-Signature']
body = request.raw_body
secret = 'your-webhook-secret'

if client.webhook.verify_signature(signature, body, secret)
  # Process the webhook
else
  # Invalid signature
end
```

## 8. Command-line Tool

```ruby
# Send an SMS
ccai --client-id YOUR-CLIENT-ID --api-key YOUR-API-KEY \
     --first-name John --last-name Doe --phone +15551234567 \
     --message "Hello ${firstName}, this is a test message!" \
     --title "CLI Test"

# Send an MMS
ccai --type mms --client-id YOUR-CLIENT-ID --api-key YOUR-API-KEY \
     --first-name John --last-name Doe --phone +15551234567 \
     --message "Hello ${firstName}, check out this image!" \
     --title "CLI Test" \
     --image path/to/your/image.jpg --content-type image/jpeg

# Send an Email
ccai --type email --client-id YOUR-CLIENT-ID --api-key YOUR-API-KEY \
     --first-name John --last-name Doe --email john@example.com \
     --subject "Welcome" --message "<p>Hello ${firstName}!</p>" \
     --sender-email noreply@yourcompany.com --reply-email support@yourcompany.com \
     --sender-name "Your Company" --title "Welcome Email"
```

## 9. Contact Validator

Validate email addresses and phone numbers.

> Bulk endpoints accept up to 50 contacts per request and are processed server-side in chunks.

```ruby
require 'ccai'

client = CCAI.new(
  client_id: 'YOUR-CLIENT-ID',
  api_key: 'YOUR-API-KEY'
)

# Validate a single email
email_result = client.contact_validator.validate_email('user@example.com')
puts "Status: #{email_result['status']}" # "valid" | "invalid" | "risky"

# Validate multiple emails (up to 50)
bulk_emails = client.contact_validator.validate_emails(['user@example.com', 'bad@invalid.xyz'])
puts "Total: #{bulk_emails['summary']['total']}" # 2
puts "Valid: #{bulk_emails['summary']['valid']}"  # 1

# Validate a single phone number
phone_result = client.contact_validator.validate_phone('+15551234567', country_code: 'US')
puts "Status: #{phone_result['status']}" # "valid" | "invalid" | "landline"

# Validate multiple phone numbers (up to 50)
bulk_phones = client.contact_validator.validate_phones([
  { phone: '+15551234567' },
  { phone: '+15559876543', countryCode: 'US' }
])
puts "Landline: #{bulk_phones['summary']['landline']}" # 1
```

## 10. Brand Registration

Register and manage brands for TCR verification.

```ruby
require 'ccai'

client = CCAI.new(
  client_id: 'YOUR-CLIENT-ID',
  api_key: 'YOUR-API-KEY'
)

# Create a brand
brand = client.brands.create(
  legalCompanyName: 'Collect.org Inc.',
  dba: 'Collect',
  entityType: 'NON_PROFIT',
  taxId: '123456789',
  taxIdCountry: 'US',
  country: 'US',
  verticalType: 'NON_PROFIT',
  websiteUrl: 'https://www.collect.org',
  street: '123 Main Street',
  city: 'San Francisco',
  state: 'CA',
  postalCode: '94105',
  contactFirstName: 'Jane',
  contactLastName: 'Doe',
  contactEmail: 'jane@collect.org',
  contactPhone: '+14155551234'
)
puts "Brand created with ID: #{brand['id']}"

# Get a brand by ID
fetched = client.brands.get(brand['id'])
puts "Brand name: #{fetched['legalCompanyName']}"

# List all brands
brands = client.brands.list
puts "Total brands: #{brands.length}"

# Update a brand (partial update)
client.brands.update(brand['id'],
  street: '456 Oak Avenue',
  city: 'Los Angeles'
)

# Delete a brand
client.brands.delete(brand['id'])
```

**Entity Types:** `PRIVATE_PROFIT`, `PUBLIC_PROFIT`, `NON_PROFIT`, `GOVERNMENT`, `SOLE_PROPRIETOR`

**Vertical Types:** `AUTOMOTIVE`, `AGRICULTURE`, `BANKING`, `COMMUNICATION`, `CONSTRUCTION`, `EDUCATION`, `ENERGY`, `ENTERTAINMENT`, `GOVERNMENT`, `HEALTHCARE`, `HOSPITALITY`, `INSURANCE`, `LEGAL`, `MANUFACTURING`, `NON_PROFIT`, `PROFESSIONAL`, `REAL_ESTATE`, `RETAIL`, `TECHNOLOGY`, `TRANSPORTATION`

## 10. Campaign Registration

Register and manage campaigns for TCR carrier vetting.

```ruby
require 'ccai'

client = CCAI.new(
  client_id: 'YOUR-CLIENT-ID',
  api_key: 'YOUR-API-KEY'
)

# Create a campaign
campaign = client.campaigns.create(
  brandId: 1,
  useCase: 'MIXED',
  subUseCases: ['CUSTOMER_CARE', 'TWO_FACTOR_AUTHENTICATION', 'ACCOUNT_NOTIFICATION'],
  description: 'Security codes and support messaging.',
  messageFlow: 'Users opt-in via signup form at https://example.com/signup',
  hasEmbeddedLinks: true,
  hasEmbeddedPhone: false,
  isAgeGated: false,
  isDirectLending: false,
  optInKeywords: ['START'],
  optInMessage: 'Welcome! Reply STOP to cancel.',
  optInProofUrl: 'https://example.com/opt-in-proof.png',
  helpKeywords: ['HELP'],
  helpMessage: 'For HELP email support@example.com.',
  optOutKeywords: ['STOP'],
  optOutMessage: 'STOP received. You are unsubscribed.',
  sampleMessages: [
    'Your code is 554321. Reply STOP to cancel.',
    'Your ticket has been updated. Reply HELP for info.'
  ]
)
puts "Campaign created with ID: #{campaign['id']}"

# Get a campaign by ID
fetched = client.campaigns.get(campaign['id'])
puts "Campaign use case: #{fetched['useCase']}"

# List all campaigns
campaigns = client.campaigns.list
puts "Total campaigns: #{campaigns.length}"

# Update a campaign (partial update)
client.campaigns.update(campaign['id'],
  description: 'Updated description.'
)

# Delete a campaign
client.campaigns.delete(campaign['id'])
```

**Use Cases:** `TWO_FACTOR_AUTHENTICATION`, `ACCOUNT_NOTIFICATION`, `CUSTOMER_CARE`, `DELIVERY_NOTIFICATION`, `FRAUD_ALERT`, `HIGHER_EDUCATION`, `LOW_VOLUME_MIXED`, `MARKETING`, `MIXED`, `POLLING_VOTING`, `PUBLIC_SERVICE_ANNOUNCEMENT`, `SECURITY_ALERT`

> `MIXED` and `LOW_VOLUME_MIXED` campaigns require 2–3 `subUseCases`.

**Sub-Use Cases:** `TWO_FACTOR_AUTHENTICATION`, `ACCOUNT_NOTIFICATION`, `CUSTOMER_CARE`, `DELIVERY_NOTIFICATION`, `FRAUD_ALERT`, `MARKETING`, `POLLING_VOTING`

## 11. Project Structure

* **lib/ -** Library code
  * **ccai.rb -** Main entry point
  * **ccai/ -** Core library files
    * **version.rb -** Version information
    * **client.rb -** Main CCAI client
    * **sms/ -** SMS-related functionality
      * **models.rb -** Data models
      * **sms_service.rb -** SMS service implementation
      * **mms_service.rb -** MMS service implementation
    * **email/ -** Email-related functionality
      * **email_service.rb -** Email service implementation
    * **webhook_service.rb - **Webhook service implementation
* **bin/ -** Command-line tools
  * **ccai -** Command-line interface
* **examples/ -** Example usage
  * **sms_send.rb -** Basic SMS example
  * **mms_send.rb -** MMS examples
  * **email_example.rb -** Email campaign examples
  * **webhook_example.rb -** Webhook management examples
  * **progress_tracking_example.rb -** Progress tracking example
* **test/ -** Test files

## 12. Features

* Send SMS messages to single or multiple recipients
* Send MMS messages with images
* Send email campaigns with HTML content
* Upload images to S3 with signed URLs
* Manage webhooks for real-time event notifications
* Variable substitution in messages
* Progress tracking via callbacks
* Comprehensive error handling
* Full test coverage
* Command-line interface for SMS, MMS, and Email

## 13. Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake test` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`.

## Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-ruby).
