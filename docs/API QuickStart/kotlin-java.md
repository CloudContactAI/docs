---
title: Kotlin/Java
excerpt: A Kotlin/Java client library for interacting with the CloudContactAI API.
deprecated: false
hidden: false
metadata:
  title: Send emails, SMS, and MMS with Java - CloudContactAI
  description: >-
    Learn how to send your first email, SMS, and MMS using the CloudContactAI
    Kotlin/Java SDK
  image: >-
    https://files.readme.io/a5190d507936a4d6cf838dbf1d065aeacb7db8c29867dfcffb47e319cf32827d-Group_14.png
  keywords:
    - email
    - mms
    - sms
    - api
    - Java
    - Kotlin
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
    <version>1.0.5</version>
</dependency>
```

### Gradle

Add the following to your `build.gradle`:

```
implementation 'com.cloudcontactai:ccai-java:1.0.5'
```

## 2. Configuration

Set environment variables or pass configuration directly:

```kotlin
export CCAI_CLIENT_ID=1231
export CCAI_API_KEY=your-api-key-here
export CCAI_USE_TEST_ENVIRONMENT=false
```

## 3. Usage

### Springboot Integration

#### Configuration Bean

```kotlin
@Configuration
class CCAIConfiguration {
    
    @Bean
    fun ccaiConfig(
        @Value("\${ccai.client-id}") clientId: String,
        @Value("\${ccai.api-key}") apiKey: String,
        @Value("\${ccai.use-test-environment:false}") useTestEnvironment: Boolean
    ): CCAIConfig {
        return CCAIConfig(
            clientId = clientId,
            apiKey = apiKey,
            useTestEnvironment = useTestEnvironment
        )
    }
    
    @Bean
    fun ccaiClient(config: CCAIConfig): CCAIClient {
        return CCAIClient(config)
    }
}
```

#### Service Bean

```kotlin
@Service
class NotificationService(private val ccaiClient: CCAIClient) {
    
    fun sendWelcomeSMS(firstName: String, lastName: String, phone: String) {
        val response = ccaiClient.sms.sendSingle(
            firstName = firstName,
            lastName = lastName,
            phone = phone,
            message = "Welcome ${firstName}! Thanks for joining our service.",
            title = "Welcome SMS"
        )
        println("SMS sent with ID: ${response.id}")
    }
    
    fun sendWelcomeEmail(firstName: String, lastName: String, email: String) {
        val response = ccaiClient.email.sendSingle(
            firstName = firstName,
            lastName = lastName,
            email = email,
            subject = "Welcome ${firstName}!",
            htmlContent = """
                <html>
                    <body>
                        <h1>Welcome ${firstName} ${lastName}!</h1>
                        <p>Thank you for joining our service.</p>
                    </body>
                </html>
            """.trimIndent()
        )
        println("Email sent with ID: ${response.id}")
    }
}
```

#### Application Properties

```kotlin
ccai.client-id=${CCAI_CLIENT_ID}
ccai.api-key=${CCAI_API_KEY}
ccai.use-test-environment=false
```

### Koltin Usage

#### SMS Basic Usage

```kotlin
import com.cloudcontactai.sdk.CCAIClient
import com.cloudcontactai.sdk.common.CCAIConfig
import com.cloudcontactai.sdk.sms.Account

// Initialize the client
val config = CCAIConfig(
    clientId = System.getenv("CCAI_CLIENT_ID") ?: throw IllegalArgumentException("CCAI_CLIENT_ID not found"),
    apiKey = System.getenv("CCAI_API_KEY") ?: throw IllegalArgumentException("CCAI_API_KEY not found")
)

val ccai = CCAIClient(config)

// Send a single SMS
val response = ccai.sms.sendSingle(
    firstName = "John",
    lastName = "Doe",
    phone = "+15551234567",
    message = "Hello John, this is a test message!",
    title = "Test Campaign"
)

println("Message sent with ID: ${response.id}")

// Send to multiple recipients
val accounts = listOf(
    Account(
        firstName = "John",
        lastName = "Doe",
        phone = "+15551234567"
    ),
    Account(
        firstName = "Jane",
        lastName = "Smith",
        phone = "+15559876543"
    )
)

val campaignResponse = ccai.sms.send(
    accounts = accounts,
    message = "Hello from our service!",
    title = "Bulk Test Campaign"
)

println("Campaign sent with ID: ${campaignResponse.id}")

ccai.close()
```

<br />

#### Email Usage

```kotlin
import com.cloudcontactai.sdk.email.EmailAccount

// Send a single email
val response = ccai.email.sendSingle(
    firstName = "John",
    lastName = "Doe",
    email = "john.doe@example.com",
    subject = "Welcome John!",
    htmlContent = "<h1>Hello John Doe!</h1><p>Welcome to our service.</p>"
)

println("Email sent with ID: ${response.id}")

// Send email campaign
val emailAccounts = listOf(
    EmailAccount(
        firstName = "John",
        lastName = "Doe",
        email = "john.doe@example.com"
    ),
    EmailAccount(
        firstName = "Jane",
        lastName = "Smith",
        email = "jane.smith@example.com"
    )
)

val campaignResponse = ccai.email.send(
    accounts = emailAccounts,
    subject = "Newsletter",
    htmlContent = "<h1>Hello!</h1><p>Here's your newsletter.</p>"
)

println("Email campaign sent with ID: ${campaignResponse.id}")
```

#### MMS Usage

<br />

**Image Recommendations**

For optimal MMS delivery and performance:

**Dimensions:**

* Recommended: 640px × 1138px (9:16 aspect ratio)
* Alternative: 1080px × 1920px (9:16 aspect ratio)
* Format: Portrait or square orientation preferred

**File Size:**

* Target: ~200 KB (optimal for speed and deliverability)
* Maximum: 1 MB
* Use image compression tools to reduce file size while maintaining quality

**Supported Formats:**

* JPEG (recommended)****
* PNG
* GIF

**Best Practice:** Keep images under 500 KB with 640×1138px dimensions for optimal compatibility and performance.

**Code Examples**

```kotlin
import com.cloudcontactai.sdk.mms.Account
import java.io.File

// Send MMS with automatic image upload (recommended)
val mmsAccounts = listOf(
    Account(
        firstName = "John",
        lastName = "Doe",
        phone = "+15551234567"
    )
)

val imageFile = File("path/to/image.jpg")
val mmsResponse = ccai.mms.sendWithImage(
    accounts = mmsAccounts,
    message = "Check out this image!",
    title = "MMS Campaign",
    imageFile = imageFile
)

// Response ID may be in campaignId or id field
val responseId = mmsResponse.campaignId ?: mmsResponse.id
println("MMS sent with ID: ${responseId}")
```

#### Webhook Management

```kotlin
import com.cloudcontactai.sdk.webhook.WebhookRequest

// Create a webhook (auto-generated secret)
val webhook = ccai.webhook.create(WebhookRequest("https://your-app.com/webhooks/ccai"))
println("Webhook created with ID: ${webhook.id}")
println("URL: ${webhook.url}")
println("Secret Key: ${webhook.secretKey}")

// Create a webhook with custom secret
val customWebhook = ccai.webhook.create(
    WebhookRequest("https://your-app.com/webhooks/ccai", "my-custom-secret-32chars12345")
)
println("Webhook created with custom secret!")

// Get the webhook
val webhookDetails = ccai.webhook.get()
webhookDetails?.let {
    println("Current webhook URL: ${it.url}")
    println("Method: ${it.method}")
    println("Secret Key: ${it.secretKey}")
}

// Update webhook
val updated = ccai.webhook.update(
    WebhookRequest("https://your-app.com/webhooks/ccai-updated", "my-custom-secret-32chars12345")
)
println("Webhook updated to: ${updated.url}")

// Validate CloudContactAI webhook signature (using eventHash)
val payload = """
{
    "eventType": "sms.sent",
    "data": {
        "id": 12345,
        "MessageStatus": "sent",
        "To": "+15551234567",
        "Message": "Hello World"
    },
    "eventHash": "abc123def456ghi789jkl012mno345pq"
}
"""
val signature = request.getHeader("X-CCAI-Signature")
val event = ccai.webhook.parseWebhookEvent(payload)

val isValid = ccai.webhook.validateSignature(
    signature,
    webhook.secretKey!!,
    config.clientId.toLong(),
    event.eventHash
)

if (isValid) {
    println("Event type: ${event.eventType}")
    println("Event hash: ${event.eventHash}")
    println("Data: ${event.data}")
}
```

### Java Usage

```kotlin
import com.cloudcontactai.sdk.CCAIClient;
import com.cloudcontactai.sdk.common.CCAIConfig;
import com.cloudcontactai.sdk.sms.SMSResponse;

// Initialize the client
CCAIConfig config = new CCAIConfig(
    System.getenv("CCAI_CLIENT_ID"),
    System.getenv("CCAI_API_KEY"),
    false  // useTestEnvironment
);

CCAIClient ccai = new CCAIClient(config);

// Send SMS
SMSResponse response = ccai.getSms().sendSingle(
    "John",
    "Doe", 
    "+15551234567",
    "Hello John, this is a test message!",
    "Test Campaign",
    null  // optional sender phone
);

System.out.println("Message sent with ID: " + response.getId());

ccai.close();
```

## 4. Configuration Options

The `CCAIConfig` class supports the following options:

* `clientId`: Your CCAI client ID (required)
* `apiKey`: Your CCAI API key (required)
* `useTestEnvironment`: Whether to use test environment URLs (default: false)
* `debugMode`: Enable debug logging (default: false)
* `maxRetries`: Maximum retry attempts for failed requests (default: 3)
* `timeoutMs`: Request timeout in milliseconds (default: 30000)

The SDK automatically configures the following URLs based on `useTestEnvironment`:

* `baseUrl`: SMS/MMS API endpoint
* `emailBaseUrl`: Email API endpoint
* `authBaseUrl`: Authentication API endpoint
* `filesBaseUrl`: File upload API endpoint (for MMS)

## 5. Error Handling

The SDK throws `CCAIException` for API errors:

```kotlin
try {
    val response = ccai.sms.sendSingle(
        firstName = "John",
        lastName = "Doe",
        phone = "invalid-phone",
        message = "Test message",
        title = "Test"
    )
} catch (e: CCAIException) {
    println("API Error: ${e.message}")
}
```

## 6. Building from Source

```kotlin
git clone https://github.com/cloudcontactai/ccai-java-sdk.git
cd ccai-java-sdk
mvn clean install
```

## 7. Testing

```kotlin
mvn test
```

<br />

## 8. License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/CloudContactAI/ccai-java/blob/main/LICENSE) file for details.

## &#x20;Try it Yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-node).