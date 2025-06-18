---
title: Go
excerpt: Send SMS or MMS with Go
deprecated: false
hidden: false
metadata:
  robots: index
---
Learn how to send your first SMS or MMS using the CCAI Go SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Paid Plan
* Create an API Key
* Get your Client ID
* Watch this video if you need help
* <Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />
  <br />

## 1. Install

Get the CCAI Go SDK.

```text
go get github.com/cloudcontactai/ccai-go
```

## 2. Send SMS message

```go
package main

import (
	"fmt"
	"log"

	"github.com/cloudcontactai/ccai-go/pkg/ccai"
	"github.com/cloudcontactai/ccai-go/pkg/sms"
)

func main() {
	// Initialize the client
	client, err := ccai.NewClient(ccai.Config{
		ClientID: "YOUR-CLIENT-ID",
		APIKey:   "YOUR-API-KEY",
	})
	if err != nil {
		log.Fatalf("Failed to create CCAI client: %v", err)
	}

	// Send a single SMS
	response, err := client.SMS.SendSingle(
		"John",
		"Doe",
		"+15551234567",
		"Hello ${firstName}, this is a test message!",
		"Test Campaign",
		nil,
	)
	if err != nil {
		log.Fatalf("Failed to send SMS: %v", err)
	}

	fmt.Printf("Message sent with ID: %s\n", response.ID)

	// Send to multiple recipients
	accounts := []sms.Account{
		{
			FirstName: "John",
			LastName:  "Doe",
			Phone:     "+15551234567",
		},
		{
			FirstName: "Jane",
			LastName:  "Smith",
			Phone:     "+15559876543",
		},
	}

	campaignResponse, err := client.SMS.Send(
		accounts,
		"Hello ${firstName} ${lastName}, this is a test message!",
		"Bulk Test Campaign",
		nil,
	)
	if err != nil {
		log.Fatalf("Failed to send bulk SMS: %v", err)
	}

	fmt.Printf("Campaign sent with ID: %s\n", campaignResponse.CampaignID)
}
```

<br />

## 3. Send MMS message

```go
package main

import (
	"fmt"
	"log"

	"github.com/cloudcontactai/ccai-go/pkg/ccai"
	"github.com/cloudcontactai/ccai-go/pkg/sms"
)

func main() {
	// Initialize the client
	client, err := ccai.NewClient(ccai.Config{
		ClientID: "YOUR-CLIENT-ID",
		APIKey:   "YOUR-API-KEY",
	})
	if err != nil {
		log.Fatalf("Failed to create CCAI client: %v", err)
	}

	// Define progress tracking
	options := &sms.Options{
		Timeout: 60,
		OnProgress: func(status string) {
			fmt.Printf("Progress: %s\n", status)
		},
	}

	// Complete MMS workflow (get URL, upload image, send MMS)
	imagePath := "path/to/your/image.jpg"
	contentType := "image/jpeg"

	// Define recipient
	account := sms.Account{
		FirstName: "John",
		LastName:  "Doe",
		Phone:     "+15551234567",  // Use E.164 format
	}

	// Send MMS with image in one step
	response, err := client.MMS.SendWithImage(
		imagePath,
		contentType,
		[]sms.Account{account},
		"Hello ${firstName}, check out this image!",
		"MMS Campaign Example",
		options,
		true,
	)
	if err != nil {
		log.Fatalf("Error sending MMS: %v", err)
	}

	fmt.Printf("MMS sent! Campaign ID: %s\n", response.CampaignID)
}
```

## 4. Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-go).