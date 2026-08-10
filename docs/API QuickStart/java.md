---
title: Java
excerpt: Send SMS with Java
deprecated: false
hidden: false
metadata:
  title: Send emails, SMS, and MMS with Java - CloudContactAI
  description: >-
    Learn how to send your first email, SMS, and MMS using the CloudContactAI
    Java SDK
  image: >-
    https://files.readme.io/a5190d507936a4d6cf838dbf1d065aeacb7db8c29867dfcffb47e319cf32827d-Group_14.png
  keywords:
    - email
    - mms
    - sms
    - api
    - Java
  robots: index
---
> 🔑 [Get API Key](https://app.cloudcontactai.com/register)

A Java client library for interacting with the CloudContactAI API using Spring Boot.

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Trial Account [here](https://app.cloudcontactai.com/register)
* Get your Client ID from Account\Settings
* Create\Copy an API Key from Account Settings

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />

## 1. Install

### Maven

Add the following dependency to your `pom.xml` :

```xml
<dependency>
    <groupId>com.cloudcontactai</groupId>
    <artifactId>ccai-java</artifactId>
    <version>1.0.0</version>
</dependency>
```

### Gradle

Add the following to your `build.gradle`:

```
implementation 'com.cloudcontactai:ccai-java:1.0.0'
```

## 2. Configuration

### Environmental Variables

Create a `.env` file in your project root or set environment variables:

```java
CCAI_CLIENT_ID=1231
CCAI_API_KEY=your-api-key-here
CCAI_BASE_URL=https://core.cloudcontactai.com/api
CCAI_EMAIL_BASE_URL=https://email-campaigns.cloudcontactai.com
CCAI_AUTH_BASE_URL=https://auth.cloudcontactai.com
```

### Application Properties

Add to your `application.properties`:

```java
ccai.client-id=${CCAI_CLIENT_ID}
ccai.api-key=${CCAI_API_KEY}
ccai.base-url=${CCAI_BASE_URL:https://core.cloudcontactai.com/api}
ccai.email-base-url=${CCAI_EMAIL_BASE_URL:https://email-campaigns.cloudcontactai.com}
ccai.auth-base-url=${CCAI_AUTH_BASE_URL:https://auth.cloudcontactai.com}
ccai.debug-mode=false
ccai.timeout-ms=30000
ccai.max-retries=3
```

## 3. Usage

### SMS Basic Usage

```java
import com.cloudcontactai.ccai.client.CCAIClient;
import com.cloudcontactai.ccai.sms.SMSResponse;
import com.cloudcontactai.ccai.exception.CCAIApiException;

// Initialize the client
CCAIClient client = CCAIClient.builder()
    .clientId("your-client-id")
    .apiKey("your-api-key")
    .debugMode(true)
    .build();

try {
    // Send SMS to a single number
    SMSResponse response = client.getSmsService().sendSMS(
        "+1234567890", 
        "Hello from CCAI Java!"
    );
    
    System.out.println("SMS sent successfully: " + response.getCampaignId());
    
} catch (CCAIApiException e) {
    System.err.println("Failed to send SMS: " + e.getMessage());
}
```

### SMS Bulk Usage

```java
import java.util.Arrays;
import java.util.List;

List<String> phoneNumbers = Arrays.asList("+1234567890", "+0987654321");

SMSResponse response = client.getSmsService().sendSMS(
    phoneNumbers,
    "Hello everyone from CCAI Java!"
);

System.out.println("Sent to " + response.getSentCount() + " numbers");
System.out.println("Failed: " + response.getFailedCount() + " numbers");
```

### SMS Advanced Usage

```java
import com.cloudcontactai.ccai.sms.SMSRequest;
import java.util.HashMap;
import java.util.Map;

SMSRequest request = new SMSRequest();
request.setPhoneNumbers(Arrays.asList("+1234567890"));
request.setMessage("Hello {{name}}, your order {{order_id}} is ready!");
request.setCampaignId("welcome-campaign");

// Add custom data
Map<String, Object> customData = new HashMap<>();
customData.put("user_id", "12345");
customData.put("order_id", "ORD-789");
request.setCustomData(customData);

SMSResponse response = client.getSmsService().sendSMS(request);
```

### SMS Async Usage

```java
import java.util.concurrent.CompletableFuture;

CompletableFuture<SMSResponse> future = client.getSmsService().sendSMSAsync(
    "+1234567890",
    "Async SMS message!"
);

future.thenAccept(response -> {
    System.out.println("Async SMS sent: " + response.getCampaignId());
}).exceptionally(throwable -> {
    System.err.println("Async SMS failed: " + throwable.getMessage());
    return null;
});
```

### Email Basic Usage

```java
import com.cloudcontactai.ccai.email.EmailResponse;

EmailResponse response = client.getEmailService().sendEmail(
    "recipient@example.com",
    "Hello from CCAI Java",
    "<h1>Hello!</h1><p>This is a test email from CCAI Java.</p>"
);

System.out.println("Email sent: " + response.getMessageId());
```

### Email Advanced Usage

```java
import com.cloudcontactai.ccai.email.EmailRequest;

EmailRequest request = new EmailRequest();
request.setToEmails(Arrays.asList("user@example.com"));
request.setSubject("Welcome to Our Service");
request.setHtmlContent("<h1>Welcome {{name}}!</h1><p>Thanks for joining us.</p>");
request.setTextContent("Welcome {{name}}! Thanks for joining us.");
request.setFromEmail("noreply@yourcompany.com");
request.setFromName("Your Company");
request.setReplyTo("support@yourcompany.com");

// Add variables for template substitution
Map<String, String> variables = new HashMap<>();
variables.put("name", "John Doe");
request.setVariables(variables);

EmailResponse response = client.getEmailService().sendEmail(request);
```

### Webhook Handling

```java
import com.cloudcontactai.ccai.webhook.WebhookEvent;
import com.cloudcontactai.ccai.webhook.WebhookService;
import org.springframework.web.bind.annotation.*;

@RestController
public class WebhookController {
    
    private final WebhookService webhookService;
    
    public WebhookController(CCAIClient client) {
        this.webhookService = client.getWebhookService();
    }
    
    @PostMapping("/webhook/ccai")
    public ResponseEntity<String> handleWebhook(
            @RequestBody String payload,
            @RequestHeader(value = "X-CCAI-Signature", required = false) String signature) {
        
        try {
            // Validate signature (optional but recommended)
            String webhookSecret = System.getenv("CCAI_WEBHOOK_SECRET");
            if (webhookSecret != null && !webhookService.validateWebhookSignature(payload, signature, webhookSecret)) {
                return ResponseEntity.status(401).body("Invalid signature");
            }
            
            // Parse and handle the event
            WebhookEvent event = webhookService.parseWebhookEvent(payload);
            webhookService.handleWebhookEvent(event);
            
            return ResponseEntity.ok("Webhook processed");
            
        } catch (Exception e) {
            return ResponseEntity.status(500).body("Error: " + e.getMessage());
        }
    }
}
```

## 5. Springboot Integration

### Auto Configuration

The library provides auto-configuration for Spring Boot applications. Simply add the dependency and configure the properties:

```java
@SpringBootApplication
public class MyApplication {
    
    @Autowired
    private CCAIClient ccaiClient;
    
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
    
    @EventListener(ApplicationReadyEvent.class)
    public void sendWelcomeSMS() throws CCAIApiException {
        SMSResponse response = ccaiClient.getSmsService().sendSMS(
            "+1234567890",
            "Application started successfully!"
        );
        System.out.println("Welcome SMS sent: " + response.getCampaignId());
    }
}
```

### Custom Configuration

```java
@Configuration
public class CCAIConfiguration {
    
    @Bean
    @Primary
    public CCAIClient customCCAIClient() {
        return CCAIClient.builder()
            .clientId(System.getenv("CCAI_CLIENT_ID"))
            .apiKey(System.getenv("CCAI_API_KEY"))
            .debugMode(true)
            .timeoutMs(60000)
            .maxRetries(5)
            .build();
    }
}
```

## 6. Error Handling

```java
import com.cloudcontactai.ccai.exception.CCAIApiException;

try {
    SMSResponse response = client.getSmsService().sendSMS("+1234567890", "Test");
} catch (CCAIApiException e) {
    System.err.println("API Error: " + e.getMessage());
    System.err.println("Status Code: " + e.getStatusCode());
    System.err.println("Error Code: " + e.getErrorCode());
}
```

## 7. Testing

Run the tests with Maven:

```text
mvn test
```

Run with coverage:

```
mvn test jacoco:report
```

<br />

## 8. Examples

The `src/main/java/com/cloudcontactai/ccai/examples` directory contains complete examples:

* `BasicSMSExample.java` - Basic SMS sending examples
* `BasicEmailExample.java` - Basic email sending examples
* `WebhookExample.java` - Complete webhook handling server

To run the examples:

```java
# Set environment variables
export CCAI_CLIENT_ID="your-client-id"
export CCAI_API_KEY="your-api-key"

# Run SMS example
mvn exec:java -Dexec.mainClass="com.cloudcontactai.ccai.examples.BasicSMSExample"

# Run email example
mvn exec:java -Dexec.mainClass="com.cloudcontactai.ccai.examples.BasicEmailExample"

# Run webhook server
mvn spring-boot:run -Dspring-boot.run.mainClass="com.cloudcontactai.ccai.examples.WebhookExample"

```

## 9. Building

Build the project:

```
mvn clean compile
```

Package the JAR:

```
mvn clean package
```

Install to local repository:

```
mvn clean install
```

## 10. Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for your changes
5. Ensure all tests pass
6. Submit a pull request

## 11. License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/CloudContactAI/ccai-java/blob/main/LICENSE) file for details.

## 12. Contact Validator

Validate email addresses and phone numbers.

> Bulk endpoints accept up to 50 contacts per request and are processed server-side in chunks.

```kotlin
import com.cloudcontactai.sdk.contactvalidator.PhoneInput

// Validate a single email
val emailResult = ccai.contactValidator.validateEmail("user@example.com")
println(emailResult.status) // "valid" | "invalid" | "risky"

// Validate multiple emails (up to 50)
val bulkEmails = ccai.contactValidator.validateEmails(listOf(
    "user@example.com",
    "bad@invalid.xyz"
))
println(bulkEmails.summary) // ValidationSummary(total=2, valid=1, invalid=1, risky=0, landline=0)

// Validate a single phone number
val phoneResult = ccai.contactValidator.validatePhone("+15551234567", countryCode = "US")
println(phoneResult.status) // "valid" | "invalid" | "landline"

// Validate multiple phone numbers (up to 50)
val bulkPhones = ccai.contactValidator.validatePhones(listOf(
    PhoneInput(phone = "+15551234567"),
    PhoneInput(phone = "+15559876543", countryCode = "US")
))
println(bulkPhones.summary) // ValidationSummary(total=2, valid=1, invalid=0, risky=0, landline=1)
```

## 13. Brand Registration

Register and manage brands for TCR verification.

```kotlin
import com.cloudcontactai.sdk.brands.BrandRequest

// Create a brand
val brand = ccai.brands.create(BrandRequest(
    legalCompanyName = "Collect.org Inc.",
    dba = "Collect",
    entityType = "NON_PROFIT",
    taxId = "123456789",
    taxIdCountry = "US",
    country = "US",
    verticalType = "NON_PROFIT",
    websiteUrl = "https://www.collect.org",
    street = "123 Main Street",
    city = "San Francisco",
    state = "CA",
    postalCode = "94105",
    contactFirstName = "Jane",
    contactLastName = "Doe",
    contactEmail = "jane@collect.org",
    contactPhone = "+14155551234"
))
println("Brand created with ID: ${brand.id}")

// Get a brand by ID
val fetched = ccai.brands.get(brand.id)
println("Brand name: ${fetched.legalCompanyName}")

// List all brands
val brands = ccai.brands.list()
println("Total brands: ${brands.size}")

// Update a brand (partial update)
ccai.brands.update(brand.id, BrandRequest(
    street = "456 Oak Avenue",
    city = "Los Angeles"
))

// Delete a brand
ccai.brands.delete(brand.id)
```

**Entity Types:** `PRIVATE_PROFIT`, `PUBLIC_PROFIT`, `NON_PROFIT`, `GOVERNMENT`, `SOLE_PROPRIETOR`

**Vertical Types:** `AUTOMOTIVE`, `AGRICULTURE`, `BANKING`, `COMMUNICATION`, `CONSTRUCTION`, `EDUCATION`, `ENERGY`, `ENTERTAINMENT`, `GOVERNMENT`, `HEALTHCARE`, `HOSPITALITY`, `INSURANCE`, `LEGAL`, `MANUFACTURING`, `NON_PROFIT`, `PROFESSIONAL`, `REAL_ESTATE`, `RETAIL`, `TECHNOLOGY`, `TRANSPORTATION`

## 14. Campaign Registration

Register and manage campaigns for TCR carrier vetting.

```kotlin
import com.cloudcontactai.sdk.campaigns.CampaignRequest

// Create a campaign
val campaign = ccai.campaigns.create(CampaignRequest(
    brandId = 1,
    useCase = "MIXED",
    subUseCases = listOf("CUSTOMER_CARE", "TWO_FACTOR_AUTHENTICATION", "ACCOUNT_NOTIFICATION"),
    description = "Security codes and support messaging.",
    messageFlow = "Users opt-in via signup form at https://example.com/signup",
    hasEmbeddedLinks = true,
    hasEmbeddedPhone = false,
    isAgeGated = false,
    isDirectLending = false,
    optInKeywords = listOf("START"),
    optInMessage = "Welcome! Reply STOP to cancel.",
    optInProofUrl = "https://example.com/opt-in-proof.png",
    helpKeywords = listOf("HELP"),
    helpMessage = "For HELP email support@example.com.",
    optOutKeywords = listOf("STOP"),
    optOutMessage = "STOP received. You are unsubscribed.",
    sampleMessages = listOf(
        "Your code is 554321. Reply STOP to cancel.",
        "Your ticket has been updated. Reply HELP for info."
    )
))
println("Campaign created with ID: ${campaign.id}")

// Get a campaign by ID
val fetched = ccai.campaigns.get(campaign.id)
println("Campaign use case: ${fetched.useCase}")

// List all campaigns
val campaigns = ccai.campaigns.list()
println("Total campaigns: ${campaigns.size}")

// Update a campaign (partial update)
ccai.campaigns.update(campaign.id, CampaignRequest(
    description = "Updated description."
))

// Delete a campaign
ccai.campaigns.delete(campaign.id)
```

**Use Cases:** `TWO_FACTOR_AUTHENTICATION`, `ACCOUNT_NOTIFICATION`, `CUSTOMER_CARE`, `DELIVERY_NOTIFICATION`, `FRAUD_ALERT`, `HIGHER_EDUCATION`, `LOW_VOLUME_MIXED`, `MARKETING`, `MIXED`, `POLLING_VOTING`, `PUBLIC_SERVICE_ANNOUNCEMENT`, `SECURITY_ALERT`

> `MIXED` and `LOW_VOLUME_MIXED` campaigns require 2–3 `subUseCases`.

**Sub-Use Cases:** `TWO_FACTOR_AUTHENTICATION`, `ACCOUNT_NOTIFICATION`, `CUSTOMER_CARE`, `DELIVERY_NOTIFICATION`, `FRAUD_ALERT`, `MARKETING`, `POLLING_VOTING`

## &#x20;Try it yourself

See the full source code [here](https://github.com/cloudcontactai/ccai-java).
