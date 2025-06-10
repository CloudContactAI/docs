---
title: Python
excerpt: Send SMS with Python
deprecated: false
hidden: false
metadata:
  robots: index
---
Learn how to send your first SMS using the CCAI Python SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Paid Plan
* Create an API Key

## 1. Install

Get the CCAI Python SDK

```node
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

## 3. Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-python).