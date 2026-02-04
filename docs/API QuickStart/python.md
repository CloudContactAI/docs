---
title: Python
excerpt: Send SMS with Python
deprecated: false
hidden: false
metadata:
  title: Send emails, SMS, and MMS with Python - CloudContactAI
  description: >-
    Learn how to send your first email, SMS, and MMS using the CloudContactAI
    Python SDK
  image: >-
    https://files.readme.io/ca2fb6972a15bc44e0b15a63fc2636c6425ccb123c26a22213dec5f627006a72-Group_14.png
  keywords:
    - email
    - sms
    - mms
    - python
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

Learn how to send your first SMS using the CCAI Python SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Trial Account [here](https://app.cloudcontactai.com/register)
* Get your Client ID from Account\Settings
* Create\Copy an API Key from Account Settings

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />

## 1. Install

Get the CCAI Python SDK

```text text
pip install ccai-python
```

## 2. Send SMS message

```python
from ccai_python import CCAI

# Initialize the client
ccai = CCAI(
    client_id="YOUR-CLIENT-ID",
    api_key="YOUR-API-KEY"
)

# Send a single SMS
response = ccai.sms.send_single(
    first_name="John",
    last_name="Doe",
    phone="+15551234567",
    message="Hello ${first_name}, this is a test message!",
    title="Test Campaign"
)

print(f"Message sent with ID: {response.id}")

# Send to multiple recipients
accounts = [
    {"first_name": "John", "last_name": "Doe", "phone": "+15551234567"},
    {"first_name": "Jane", "last_name": "Smith", "phone": "+15559876543"}
]

campaign_response = ccai.sms.send(
    accounts=accounts,
    message="Hello ${first_name} ${last_name}, this is a test message!",
    title="Bulk Test Campaign"
)

print(f"Campaign sent with ID: {campaign_response.campaign_id}")
```

## 3. Send MMS message

```python
from ccai_python import CCAI, Account, SMSOptions

# Initialize the client
ccai = CCAI(
    client_id="YOUR-CLIENT-ID",
    api_key="YOUR-API-KEY"
)

# Define a progress callback
def track_progress(status):
    print(f"Progress: {status}")

# Create options with progress tracking
options = SMSOptions(
    timeout=60,
    retries=3,
    on_progress=track_progress
)

# Complete MMS workflow (get URL, upload image, send MMS)
image_path = "path/to/your/image.jpg"
content_type = "image/jpeg"

# Define recipient
account = Account(
    first_name="John",
    last_name="Doe",
    phone="+15551234567"  # Use E.164 format
)

# Send MMS with image in one step
response = ccai.mms.send_with_image(
    image_path=image_path,
    content_type=content_type,
    accounts=[account],
    message="Hello ${first_name}, check out this image!",
    title="MMS Campaign Example",
    options=options
)

print(f"MMS sent! Campaign ID: {response.campaign_id}")
```

## 4. Send Email

```python
from ccai_python import CCAI, EmailAccount, EmailCampaign
from datetime import datetime, timedelta

# Initialize the client
ccai = CCAI(
    client_id="YOUR-CLIENT-ID",
    api_key="YOUR-API-KEY"
)

# Send a single email
response = ccai.email.send_single(
    first_name="John",
    last_name="Doe",
    email="john@example.com",
    subject="Welcome to Our Service",
    message="<p>Hello John,</p><p>Thank you for signing up!</p>",
    sender_email="noreply@yourcompany.com",
    reply_email="support@yourcompany.com",
    sender_name="Your Company",
    title="Welcome Email"
)

print(f"Email sent with ID: {response.id}")

# Send email campaign to multiple recipients
accounts = [
    EmailAccount(
        first_name="John",
        last_name="Doe",
        email="john@example.com",
        phone=""
    ),
    EmailAccount(
        first_name="Jane",
        last_name="Smith",
        email="jane@example.com",
        phone=""
    )
]

campaign = EmailCampaign(
    subject="Monthly Newsletter",
    title="July 2025 Newsletter",
    message="<h1>Hello ${firstName}!</h1><p>Here's our monthly update...</p>",
    sender_email="newsletter@yourcompany.com",
    reply_email="support@yourcompany.com",
    sender_name="Your Company Newsletter",
    accounts=accounts
)

response = ccai.email.send_campaign(campaign)
print(f"Email campaign sent: {response}")

# Schedule an email for future delivery
tomorrow = datetime.now() + timedelta(days=1)
tomorrow = tomorrow.replace(hour=10, minute=0, second=0, microsecond=0)

scheduled_campaign = EmailCampaign(
    subject="Scheduled Email",
    title="Future Email",
    message="<p>This email was scheduled in advance!</p>",
    sender_email="scheduled@yourcompany.com",
    reply_email="support@yourcompany.com",
    sender_name="Your Company",
    accounts=[accounts[0]],
    scheduled_timestamp=tomorrow.isoformat(),
    scheduled_timezone="America/New_York"
)

response = ccai.email.send_campaign(scheduled_campaign)
print(f"Email scheduled: {response}")
```

## 5. Webhooks

```python
from ccai_python import CCAI, WebhookConfig, WebhookEventType

# Initialize the client
ccai = CCAI(
    client_id="YOUR-CLIENT-ID",
    api_key="YOUR-API-KEY"
)

# Register a webhook
config = WebhookConfig(
    url="https://your-domain.com/api/ccai-webhook",
    events=[WebhookEventType.MESSAGE_SENT, WebhookEventType.MESSAGE_RECEIVED],
    secret="your-webhook-secret"
)

webhook = ccai.webhook.register(config)
print(f"Webhook registered with ID: {webhook.id}")

# List all webhooks
webhooks = ccai.webhook.list()
print(f"Found {len(webhooks)} webhooks")

# Update a webhook
update_data = {
    "events": [WebhookEventType.MESSAGE_RECEIVED]
}
updated_webhook = ccai.webhook.update(webhook.id, update_data)
print(f"Webhook updated: {updated_webhook}")

# Delete a webhook
result = ccai.webhook.delete(webhook.id)
print(f"Webhook deleted: {result}")

# Create a webhook handler for web frameworks
def handle_message_sent(event):
    print(f"Message sent: {event.message} to {event.to}")

def handle_message_received(event):
    print(f"Message received: {event.message} from {event.from_}")

handlers = {
    'on_message_sent': handle_message_sent,
    'on_message_received': handle_message_received
}

webhook_handler = ccai.webhook.create_handler(handlers)

# Use with Flask
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/api/ccai-webhook', methods=['POST'])
def handle_webhook():
    payload = request.get_json()
    result = webhook_handler(payload)
    return jsonify(result)
```

## 6. Features

* Send SMS messages to single or multiple recipients
* Send MMS messages with images
* Send Email campaigns with HTML content
* Schedule emails for future delivery
* Webhook management (register, update, list, delete)
* Webhook event handling for web frameworks
* Upload images to S3 with signed URLs
* Variable substitution in messages
* Progress tracking callbacks
* Type hints for better IDE integration
* Comprehensive error handling

## Requirements

Python 3.10 or higher

* `requests `library
* `pydantic `library

## Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-python).
