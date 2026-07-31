---
title: Go
excerpt: Send SMS or MMS with the CloudContactAI Go SDK
deprecated: false
hidden: false
metadata:
  title: Send emails, SMS, and MMS with Go - CloudContactAI
  description: >-
    Learn how to send your first email, SMS, and MMS using the CloudContactAI Go
    SDK
  image: >-
    https://files.readme.io/6d6b3f6f85975b1c8fa771a87c77534740fc9ff180908b7e7ea32ab89154336a-Group_14.png
  keywords:
    - email
    - sms
    - mms
    - go
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

Learn how to send your first SMS or MMS using the CCAI Go SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Trial Account [here](https://app.cloudcontactai.com/register)
* Get your Client ID from Account\Settings
* Create\Copy an API Key from Account Settings

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />

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

## 4. Send MMS message

```go
package main

import (
    "fmt"
    "log"
    "os"

    "github.com/cloudcontactai/ccai-go/pkg/ccai"
    "github.com/cloudcontactai/ccai-go/pkg/sms"
    "github.com/joho/godotenv"
)

func main() {
    // Load environment variables
    err := godotenv.Load()
    if err != nil {
        log.Printf("Warning: Could not load .env file: %v", err)
    }

    // Initialize the client
    client, err := ccai.NewClient(ccai.Config{
        ClientID: os.Getenv("CCAI_CLIENT_ID"),
        APIKey:   os.Getenv("CCAI_API_KEY"),
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
		Phone:     "+14156566694",  // Use E.164 format
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

## 5. Step-by-Step MMS Workflow

```go
// Step 1: Get a signed URL for uploading
uploadResponse, err := client.MMS.GetSignedUploadURL(
	"image.jpg",
	"image/jpeg",
	"",
	true,
)
if err != nil {
	log.Fatalf("Error getting signed URL: %v", err)
}

signedURL := uploadResponse.SignedS3URL
fileKey := uploadResponse.FileKey

// Step 2: Upload the image to the signed URL
uploadSuccess, err := client.MMS.UploadImageToSignedURL(
	signedURL,
	"path/to/your/image.jpg",
	"image/jpeg",
)
if err != nil {
	log.Fatalf("Error uploading image: %v", err)
}

if uploadSuccess {
	// Step 3: Send the MMS with the uploaded image
	response, err := client.MMS.Send(
		fileKey,
		accounts,
		"Hello ${firstName}, check out this image!",
		"MMS Campaign Example",
		nil,
		true,
	)
	if err != nil {
		log.Fatalf("Error sending MMS: %v", err)
	}

	fmt.Printf("MMS sent! Campaign ID: %s\n", response.CampaignID)
}
```

## 6. With Progress Tracking

```go
// Create options with progress tracking
options := &sms.Options{
	Timeout: 60,
	Retries: 3,
	OnProgress: func(status string) {
		fmt.Printf("%s - %s\n", time.Now().Format("2006-01-02 15:04:05"), status)
	},
}

// Send SMS with progress tracking
response, err := client.SMS.Send(
	accounts,
	message,
	title,
	options,
)
```

## 7. Contact Validator

Validate email addresses and phone numbers.

> Bulk endpoints accept up to 50 contacts per request and are processed server-side in chunks.

```go
package main

import (
	"fmt"
	"log"
	"os"

	"github.com/cloudcontactai/ccai-go/src/pkg/ccai"
	"github.com/cloudcontactai/ccai-go/src/pkg/contactvalidator"
	"github.com/joho/godotenv"
)

func main() {
	_ = godotenv.Load()

	client, err := ccai.NewClient(ccai.Config{
		ClientID: os.Getenv("CCAI_CLIENT_ID"),
		APIKey:   os.Getenv("CCAI_API_KEY"),
	})
	if err != nil {
		log.Fatalf("Failed to create client: %v", err)
	}

	// Validate a single email
	emailResult, err := client.ContactValidator.ValidateEmail("user@example.com")
	if err != nil {
		log.Fatalf("Failed to validate email: %v", err)
	}
	fmt.Printf("Email status: %s\n", emailResult.Status) // "valid" | "invalid" | "risky"

	// Validate multiple emails (up to 50)
	bulkEmails, err := client.ContactValidator.ValidateEmails([]string{
		"user@example.com",
		"bad@invalid.xyz",
	})
	if err != nil {
		log.Fatalf("Failed to validate emails: %v", err)
	}
	fmt.Printf("Email summary: %+v\n", bulkEmails.Summary)

	// Validate a single phone number
	phoneResult, err := client.ContactValidator.ValidatePhone("+15551234567", "US")
	if err != nil {
		log.Fatalf("Failed to validate phone: %v", err)
	}
	fmt.Printf("Phone status: %s\n", phoneResult.Status) // "valid" | "invalid" | "landline"

	// Validate multiple phone numbers (up to 50)
	bulkPhones, err := client.ContactValidator.ValidatePhones([]contactvalidator.PhoneInput{
		{Phone: "+15551234567"},
		{Phone: "+15559876543", CountryCode: "US"},
	})
	if err != nil {
		log.Fatalf("Failed to validate phones: %v", err)
	}
	fmt.Printf("Phone summary: %+v\n", bulkPhones.Summary)
}
```

## 8. Brand Registration

Register and manage brands for TCR verification.

```go
package main

import (
	"fmt"
	"log"
	"os"

	"github.com/cloudcontactai/ccai-go/src/pkg/brands"
	"github.com/cloudcontactai/ccai-go/src/pkg/ccai"
	"github.com/joho/godotenv"
)

func strPtr(s string) *string { return &s }

func main() {
	_ = godotenv.Load()

	client, err := ccai.NewClient(ccai.Config{
		ClientID: os.Getenv("CCAI_CLIENT_ID"),
		APIKey:   os.Getenv("CCAI_API_KEY"),
	})
	if err != nil {
		log.Fatalf("Failed to create client: %v", err)
	}

	// Create a brand
	brand, err := client.Brands.Create(brands.BrandRequest{
		LegalCompanyName: strPtr("Collect.org Inc."),
		Dba:              strPtr("Collect"),
		EntityType:       strPtr("NON_PROFIT"),
		TaxId:            strPtr("123456789"),
		TaxIdCountry:     strPtr("US"),
		Country:          strPtr("US"),
		VerticalType:     strPtr("NON_PROFIT"),
		WebsiteUrl:       strPtr("https://www.collect.org"),
		Street:           strPtr("123 Main Street"),
		City:             strPtr("San Francisco"),
		State:            strPtr("CA"),
		PostalCode:       strPtr("94105"),
		ContactFirstName: strPtr("Jane"),
		ContactLastName:  strPtr("Doe"),
		ContactEmail:     strPtr("jane@collect.org"),
		ContactPhone:     strPtr("+14155551234"),
	})
	if err != nil {
		log.Fatalf("Failed to create brand: %v", err)
	}
	fmt.Printf("Brand created with ID: %d\n", brand.ID)

	// Get a brand by ID
	fetched, _ := client.Brands.Get(brand.ID)
	fmt.Printf("Brand name: %s\n", fetched.LegalCompanyName)

	// List all brands
	brandList, _ := client.Brands.List()
	fmt.Printf("Total brands: %d\n", len(brandList))

	// Update a brand (partial update)
	client.Brands.Update(brand.ID, brands.BrandRequest{
		Street: strPtr("456 Oak Avenue"),
		City:   strPtr("Los Angeles"),
	})

	// Delete a brand
	client.Brands.Delete(brand.ID)
}
```

**Entity Types:** `PRIVATE_PROFIT`, `PUBLIC_PROFIT`, `NON_PROFIT`, `GOVERNMENT`, `SOLE_PROPRIETOR`

**Vertical Types:** `AUTOMOTIVE`, `AGRICULTURE`, `BANKING`, `COMMUNICATION`, `CONSTRUCTION`, `EDUCATION`, `ENERGY`, `ENTERTAINMENT`, `GOVERNMENT`, `HEALTHCARE`, `HOSPITALITY`, `INSURANCE`, `LEGAL`, `MANUFACTURING`, `NON_PROFIT`, `PROFESSIONAL`, `REAL_ESTATE`, `RETAIL`, `TECHNOLOGY`, `TRANSPORTATION`

## 9. Campaign Registration

Register and manage campaigns for TCR carrier vetting.

```go
package main

import (
	"fmt"
	"log"
	"os"

	"github.com/cloudcontactai/ccai-go/src/pkg/campaigns"
	"github.com/cloudcontactai/ccai-go/src/pkg/ccai"
	"github.com/joho/godotenv"
)

func boolPtr(b bool) *bool { return &b }

func main() {
	_ = godotenv.Load()

	client, err := ccai.NewClient(ccai.Config{
		ClientID: os.Getenv("CCAI_CLIENT_ID"),
		APIKey:   os.Getenv("CCAI_API_KEY"),
	})
	if err != nil {
		log.Fatalf("Failed to create client: %v", err)
	}

	// Create a campaign
	campaign, err := client.Campaigns.Create(campaigns.CampaignRequest{
		BrandID:          1,
		UseCase:          "MIXED",
		SubUseCases:      []string{"CUSTOMER_CARE", "TWO_FACTOR_AUTHENTICATION", "ACCOUNT_NOTIFICATION"},
		Description:      "Security codes and support messaging.",
		MessageFlow:      "Users opt-in via signup form at https://example.com/signup",
		HasEmbeddedLinks: boolPtr(true),
		HasEmbeddedPhone: boolPtr(false),
		IsAgeGated:       boolPtr(false),
		IsDirectLending:  boolPtr(false),
		OptInKeywords:    []string{"START"},
		OptInMessage:     "Welcome! Reply STOP to cancel.",
		OptInProofUrl:    "https://example.com/opt-in-proof.png",
		HelpKeywords:     []string{"HELP"},
		HelpMessage:      "For HELP email support@example.com.",
		OptOutKeywords:   []string{"STOP"},
		OptOutMessage:    "STOP received. You are unsubscribed.",
		SampleMessages: []string{
			"Your code is 554321. Reply STOP to cancel.",
			"Your ticket has been updated. Reply HELP for info.",
		},
	})
	if err != nil {
		log.Fatalf("Failed to create campaign: %v", err)
	}
	fmt.Printf("Campaign created with ID: %d\n", campaign.ID)

	// Get a campaign by ID
	fetched, _ := client.Campaigns.Get(campaign.ID)
	fmt.Printf("Campaign use case: %s\n", fetched.UseCase)

	// List all campaigns
	campaignList, _ := client.Campaigns.List()
	fmt.Printf("Total campaigns: %d\n", len(campaignList))

	// Update a campaign (partial update)
	client.Campaigns.Update(campaign.ID, campaigns.CampaignRequest{
		Description: "Updated description.",
	})

	// Delete a campaign
	client.Campaigns.Delete(campaign.ID)
}
```

**Use Cases:** `TWO_FACTOR_AUTHENTICATION`, `ACCOUNT_NOTIFICATION`, `CUSTOMER_CARE`, `DELIVERY_NOTIFICATION`, `FRAUD_ALERT`, `HIGHER_EDUCATION`, `LOW_VOLUME_MIXED`, `MARKETING`, `MIXED`, `POLLING_VOTING`, `PUBLIC_SERVICE_ANNOUNCEMENT`, `SECURITY_ALERT`

> `MIXED` and `LOW_VOLUME_MIXED` campaigns require 2–3 `SubUseCases`.

**Sub-Use Cases:** `TWO_FACTOR_AUTHENTICATION`, `ACCOUNT_NOTIFICATION`, `CUSTOMER_CARE`, `DELIVERY_NOTIFICATION`, `FRAUD_ALERT`, `MARKETING`, `POLLING_VOTING`

## 9. Project Structure

* **src/ -** Source code
  * **pkg/ -** Package code
    * **ccai/ -** Main CCAI client package
      * **client.go -** Main CCAI client implementation
      * **ccai.go -** Type definitions and exports

    * **sms/ -** SMS-related functionality
      * **models.go -** Data models
      * **sms.go -** SMS service implementation
      * **mms.go -** MMS service implementation

    * **email/ -** Email-related functionality
      * **models.go -** Email data models
      * **email.go -** Email service implementation
  * **examples/ -** Example usage
  * **email/ -** Email example
* **.env -** Environment variables
* **.env.example -** Environment variables template

## 10. Features

* Send email messages to single or multiple recipients
* Send SMS messages to single or multiple recipients
* Send MMS messages with images
* Upload images to S3 with signed URLs
* Variable substitution in messages
* Progress tracking via callbacks
* Environment variable support with .env files
* Comprehensive error handling
* Full test coverage

## &#x20;Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-go).

<br />
