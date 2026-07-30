---
title: Perl
excerpt: Send SMS or MMS with Perl
deprecated: false
hidden: false
metadata:
  title: Send emails, SMS, and MMS with Perl - CloudContactAI
  description: >-
    Learn how to send your first email, SMS, and MMS using the CloudContactAI
    Perl SDK
  image: >-
    https://files.readme.io/d1bab7924f7126429ffa5626418d89005171ccfcfc1b375c3fc4454a273bc716-Group_14.png
  keywords:
    - email
    - sms
    - mms
    - api
    - perl
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

Learn how to send your first SMS using the CCAI Perl SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Trial Account [here](https://app.cloudcontactai.com/register)
* Get your Client ID from Account\Settings
* Create\Copy an API Key from Account Settings

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />

## 1. Install

Get the CCAI Perl SDK

```perl
git clone https://github.com/cloudcontactai/ccai-perl.git
cd ccai-perl
cpanm --installdeps .

# Set up your credentials
cp .env.example .env
# Edit .env and add your CCAI credentials

# Verify SSL configuration
perl verify_ssl.pl

# Test with examples
perl -Ilib examples/sms_send.pl
```

Install the required dependencies:

```perl
# Using cpanm (recommended) - installs all dependencies including SSL support
cpanm --installdeps .

# Or install individual modules
cpanm LWP::UserAgent JSON HTTP::Request::Common File::Basename MIME::Base64 Mozilla::CA LWP::Protocol::https IO::Socket::SSL Digest::SHA

# Or using cpan
cpan LWP::UserAgent JSON HTTP::Request::Common File::Basename MIME::Base64 Mozilla::CA LWP::Protocol::https IO::Socket::SSL Digest::SHA

```

**SSL Configuration:** The client automatically configures SSL certificates. If you encounter SSL issues, run:

```perl
perl verify_ssl.pl
```

## Alternative: install all dependencies from cpanfile

```perl
cpanm --installdeps .
```

**Note:** The SSL modules (Mozilla::CA, LWP::Protocol::https, IO::Socket::SSL) are required for secure HTTPS communication with the CCAI API.

### Configuration

#### Environmental Variables

The CCAI Perl client supports loading credentials from environment variables using a .env file:

**Step 1:** Copy Example file:

```perl
cp .env.example .env
```

**Step 2:** Edit .env with your credentials:

```perl
# CCAI API Credentials
CCAI_CLIENT_ID=your-client-id-here
CCAI_API_KEY=your-api-key-here

# Optional: Suppress LWP Content-Length warnings (set to 1 to enable)
CCAI_SUPPRESS_WARNINGS=1
```

**Step 3:** Use your code:

```perl
# CCAI API Credentials
CCAI_CLIENT_ID=your-client-id-here
CCAI_API_KEY=your-api-key-here

# Optional: Suppress LWP Content-Length warnings (set to 1 to enable)
CCAI_SUPPRESS_WARNINGS=1
```

#### Direct Configuration

You can also configure credentials directly into your code:

```perl
use CCAI;

my $ccai = CCAI->new({
    client_id => 'YOUR-CLIENT-ID',
    api_key   => 'API-KEY-TOKEN'
});
```

<br />

<br />

## 2. Send SMS message

```perl
#Update YOUR-CLIENT-ID and API-KEY-TOKEN 
#Update the account object to send messages to a valid phone number. 

use lib '.';
use CCAI;

# Initialize the client
my $ccai = CCAI->new({
    client_id => 'YOUR-CLIENT-ID',
    api_key   => 'API-KEY-TOKEN'
});

# Send an SMS to multiple recipients
my @accounts = (
    {
        firstName => "John",
        lastName  => "Doe",
        phone      => "+15551234567"
    },
    {
        firstName => "Jane",
        lastName  => "Smith", 
        phone      => "+15559876543"
    }
);

my $response = $ccai->sms->send(
    \@accounts,
    "Hello \${firstName} \${lastName}, this is a test message!",
    "Test Campaign"
);

if ($response->{success}) {
    print "SMS sent successfully! Campaign ID: " . $response->{data}->{campaign_id} . "\n";
} else {
    print "Error: " . $response->{error} . "\n";
}

# Send an SMS to a single recipient
my $single_response = $ccai->sms->send_single(
    "Jane",
    "Smith",
    "+15559876543",
    "Hi \${firstName}, thanks for your interest!",
    "Single Message Test"
);

if ($single_response->{success}) {
    print "Single SMS sent successfully!\n";
} else {
    print "Error: " . $single_response->{error} . "\n";
    }
    


```

## 3. Webhooks with CustomData

````perl
use lib '.';
use CCAI;

# Initialize the client
my $ccai = CCAI->new({
    client_id => 'YOUR-CLIENT-ID',
    api_key   => 'API-KEY-TOKEN'
});

# Process a webhook event with customData (in your webhook handler)
sub process_webhook_event {
    my ($json, $signature, $secret) = @_;
    
    # Verify the signature
    if ($ccai->webhook->verify_signature($signature, $json, $secret)) {
        # Parse the event
        my $event = $ccai->webhook->parse_event($json);
        
        if ($event && $event->{type} eq "message.sent") {
            print "Message sent to: $event->{to}\n";
            
            # Access customData for business logic
            if ($event->{customData}) {
                my $custom = $event->{customData};
                
                # Handle order-related messages
                if ($custom->{order_id}) {
                    print "Order notification sent: $custom->{order_id}\n";
                    # Update order status in your system
                    # update_order_notification_status($custom->{order_id}, 'sent');
                }
                
                # Handle appointment reminders
                if ($custom->{appointment_id}) {
                    print "Appointment reminder sent: $custom->{appointment_id}\n";
                    # Mark reminder as delivered
                    # mark_reminder_delivered($custom->{appointment_id});
                }
                
                # Customer segmentation
                if ($custom->{customer_type} eq 'premium') {
                    print "Premium customer notification delivered\n";
                    # Special handling for premium customers
                }
            }
        } elsif ($event && $event->{type} eq "message.failed") {
            print "Message failed to: $event->{to}\n";
            
            # Handle failures with context from customData
            if ($event->{customData} && $event->{customData}->{order_id}) {
                print "Order notification failed: " . $event->{customData}->{order_id} . "\n";
                # Implement fallback notification (email, etc.)
                # fallback_notification($event->{customData}->{order_id});
            }
        }
    } else {
        print "Invalid signature\n";
    }
}
### Basic SMS

```perl
use CCAI;

# Initialize the client
my $ccai = CCAI->new({
    client_id => 'YOUR-CLIENT-ID',
    api_key   => 'API-KEY-TOKEN'
});

# Send an SMS to multiple recipients
my @accounts = (
    {
        firstName => "John",
        lastName  => "Doe",
        phone      => "+15551234567"
    },
    {
        firstName => "Jane",
        lastName  => "Smith", 
        phone      => "+15559876543"
    }
);

my $response = $ccai->sms->send(
    \@accounts,
    "Hello \${firstName} \${lastName}, this is a test message!",
    "Test Campaign"
);

if ($response->{success}) {
    print "SMS sent successfully! Campaign ID: " . $response->{data}->{campaign_id} . "\n";
} else {
    print "Error: " . $response->{error} . "\n";
}

# Send an SMS to a single recipient
my $single_response = $ccai->sms->send_single(
    "Jane",
    "Smith",
    "+15559876543",
    "Hi \${firstName}, thanks for your interest!",
    "Single Message Test"
);

if ($single_response->{success}) {
    print "Single SMS sent successfully!\n";
} else {
    print "Error: " . $single_response->{error} . "\n";
}
````

<br />

<br />

## 4. Send MMS Message

```perl
#Update YOUR-CLIENT-ID and API-KEY-TOKEN 
#Update the account object to send messages to a valid phone number. 
#Update path/to/your/image.jpg to be an actual jpg file

use lib '.';
use CCAI;

# Initialize the client
my $ccai = CCAI->new({
    client_id => 'YOUR-CLIENT-ID',
    api_key   => 'API-KEY-TOKEN'
});

# Define progress callback
my $progress_callback = sub {
    my $status = shift;
    print "Progress: $status\n";
};

# Create options with progress tracking
my $options = {
    timeout     => 60000,
    on_progress => $progress_callback
};

# Complete MMS workflow (get URL, upload image, send MMS)
sub send_mms_with_image {
    # Path to your image file
    my $image_path = 'path/to/your/image.jpg';
    my $content_type = 'image/jpeg';
    
    # Define recipient
    my @accounts = ({
        firstName => 'John',
        lastName  => 'Doe',
        phone      => '+15551234567'
    });
    
    # Send MMS with image in one step
    my $response = $ccai->mms->send_with_image(
        $image_path,
        $content_type,
        \@accounts,
        "Hello \${firstName}, check out this image!",
        "MMS Campaign Example",
        $options
    );
    
    if ($response->{success}) {
        print "MMS sent! Campaign ID: " . $response->{data}->{campaign_id} . "\n";
    } else {
        print "Error sending MMS: " . $response->{error} . "\n";
    }
}

# Call the function
send_mms_with_image();
```

## 5. Sending an Email

```perl
use lib '.';
use CCAI;


# Initialize the client


my $ccai = CCAI->new({
    client_id => 'YOUR-CLIENT-ID',
    api_key   => 'API-KEY-TOKEN'
});


# Send a single email


my $response = $ccai->email->send_single(
    "John",                                    # First name
    "Doe",                                     # Last name
    "john@example.com",                        # Email address
    "Welcome to Our Service",                  # Subject
    "<p>Hello \${firstName},</p><p>Thank you for signing up!</p>",  # HTML message content
    "noreply@yourcompany.com",                 # Sender email
    "support@yourcompany.com",                 # Reply-to email
    "Your Company",                            # Sender name
    "Welcome Email"                            # Campaign title
);

if ($response->{success}) {
    print "Email sent successfully! ID: " . $response->{data}->{id} . "\n";
} else {
    print "Error: " . $response->{error} . "\n";
}


# Send an email campaign to multiple recipients


my $campaign = {
    subject => "Monthly Newsletter",
    title => "July 2025 Newsletter",
    message => "<h1>Monthly Newsletter - July 2025</h1><p>Hello \${firstName},</p>",
    sender_email => "newsletter@yourcompany.com",
    reply_email => "support@yourcompany.com",
    sender_name => "Your Company Newsletter",
    accounts => [
        {
            firstName => "John",
            lastName => "Doe",
            email => "john@example.com"
        },
        {
            firstName => "Jane",
            lastName => "Smith",
            email => "jane@example.com"
        }
    ],
    campaign_type => "EMAIL",
    add_to_list => "noList",
    contact_input => "accounts",
    from_type => "single",
    senders => []
};

my $campaign_response = $ccai->email->send_campaign($campaign);

if ($campaign_response->{success}) {
    print "Email campaign sent successfully! ID: " . $campaign_response->{data}->{id} . "\n";
} else {
    print "Error: " . $campaign_response->{error} . "\n";
    }

```

## 6. Using Webhooks

### Unified Event Handler (Recommended)

The new unified event handler processes all CloudContact webhook event types with a single callback function:

```perl
use lib '.';
use CCAI;

# Initialize the client
my $ccai = CCAI->new({
    client_id => 'YOUR-CLIENT-ID',
    api_key   => 'API-KEY-TOKEN'
});

# Register a webhook for all event types
my $webhook_response = $ccai->webhook->register({
    url => "https://example.com/webhook",
    events => [
        "message.sent", 
        "message.incoming", 
        "message.excluded",
        "message.error.carrier",
        "message.error.cloudcontact"
    ],
    secret => "your-webhook-secret"
});

if ($webhook_response->{success}) {
    print "Webhook registered! ID: " . $webhook_response->{data}->{id} . "\n";
}

# Process webhook events with unified handler
sub process_webhook_event {
    my ($json, $signature, $secret) = @_;
    
    # Verify the signature
    unless ($ccai->webhook->verify_signature($signature, $json, $secret)) {
        print "❌ Invalid signature\n";
        return;
    }
    
    # Process event with unified handler
    my $success = $ccai->webhook->handle_event($json, sub {
        my ($event_type, $data) = @_;
        
        if ($event_type eq 'message.sent') {
            print "✅ Message delivered to $data->{To}\n";
            print "   💰 Cost: \$$data->{TotalPrice}\n" if $data->{TotalPrice};
            print "   📊 Segments: $data->{Segments}\n" if $data->{Segments};
            print "   📢 Campaign: $data->{CampaignTitle}\n" if $data->{CampaignTitle};
            
        } elsif ($event_type eq 'message.incoming') {
            print "📨 Reply from $data->{From}: $data->{Message}\n";
            print "   📢 Original Campaign: $data->{CampaignTitle}\n" if $data->{CampaignTitle};
            
        } elsif ($event_type eq 'message.excluded') {
            print "⚠️  Message excluded: $data->{ExcludedReason}\n";
            print "   📞 Target: $data->{To}\n";
            
        } elsif ($event_type eq 'message.error.carrier') {
            print "❌ Carrier error $data->{ErrorCode}: $data->{ErrorMessage}\n";
            print "   📞 Target: $data->{To}\n";
            
        } elsif ($event_type eq 'message.error.cloudcontact') {
            print "🚨 System error $data->{ErrorCode}: $data->{ErrorMessage}\n";
            print "   📞 Target: $data->{To}\n";
        }
        
        # Show custom data if present
        if ($data->{CustomData} && $data->{CustomData} ne '') {
            print "   📋 Custom Data: $data->{CustomData}\n";
        }
    });
    
    unless ($success) {
        print "❌ Failed to process webhook event\n";
    }
}
Supported Event Types
message.sent - Message successfully delivered to recipient

Includes pricing information (TotalPrice) and segment count (Segments)
Contains campaign details and custom data
message.incoming - Reply received from recipient

Contains the reply message and sender information
Links back to original campaign if applicable
message.excluded - Message excluded during campaign creation

Provides exclusion reason (duplicate phone, invalid format, etc.)
Helps track why certain contacts didn't receive messages
message.error.carrier - Carrier-level delivery failure

Contains carrier error codes (30008, 30007, etc.)
Indicates network or carrier-specific issues
message.error.cloudcontact - CloudContact system error

Contains CCAI error codes (CCAI-001, CCAI-002, etc.)
Indicates account or system configuration issues
Legacy Event Processing (Backward Compatible)
# Legacy method still supported for backward compatibility
sub process_webhook_event_legacy {
    my ($json, $signature, $secret) = @_;
    
    if ($ccai->webhook->verify_signature($signature, $json, $secret)) {
        my $event = $ccai->webhook->parse_event($json);
        
        if ($event && $event->{type} eq "message.sent") {
            print "Message sent to: $event->{To}\n";
        } elsif ($event && $event->{type} eq "message.incoming") {
            print "Message received from: $event->{From}\n";
        }
    }
}
```

### Supported Event Types

<br />

* **message.sent -** Message successfully delivered to recipient
  * Includes pricing information (TotalPrice) and segment count (Segments)
  * Contains campaign details and custom data
* **message.incoming -** Reply received from recipient
  * Contains the reply message and sender information
  * Links back to original campaign if applicable
* **message.excluded -** Message excluded during campaign creation
  * Provides exclusion reason (duplicate phone, invalid format, etc.)
  * Helps track why certain contacts didn't receive messages
* **message.error.carrier -** Carrier-level delivery failure
  * Contains carrier error codes (30008, 30007, etc.)
  * Indicates network or carrier-specific issues
* **message.error.cloudcontact -** CloudContact system error
  * Contains CCAI error codes (CCAI-001, CCAI-002, etc.)
  * Indicates account or system configuration issues

### Legacy Event Processing (Backwards Compatibility)

```perl
# Legacy method still supported for backward compatibility
sub process_webhook_event_legacy {
    my ($json, $signature, $secret) = @_;
    
    if ($ccai->webhook->verify_signature($signature, $json, $secret)) {
        my $event = $ccai->webhook->parse_event($json);
        
        if ($event && $event->{type} eq "message.sent") {
            print "Message sent to: $event->{To}\n";
        } elsif ($event && $event->{type} eq "message.incoming") {
            print "Message received from: $event->{From}\n";
        }
    }
}
```

## 7. Brand Registration

Register and manage brands for TCR verification.

```perl
use lib '.';
use CCAI;

my $ccai = CCAI->new({
    client_id => 'YOUR-CLIENT-ID',
    api_key   => 'API-KEY-TOKEN'
});

# Create a brand
my $brand = $ccai->brand->create({
    legalCompanyName => 'Collect.org Inc.',
    dba              => 'Collect',
    entityType       => 'NON_PROFIT',
    taxId            => '123456789',
    taxIdCountry     => 'US',
    country          => 'US',
    verticalType     => 'NON_PROFIT',
    websiteUrl       => 'https://www.collect.org',
    street           => '123 Main Street',
    city             => 'San Francisco',
    state            => 'CA',
    postalCode       => '94105',
    contactFirstName => 'Jane',
    contactLastName  => 'Doe',
    contactEmail     => 'jane@collect.org',
    contactPhone     => '+14155551234',
});

if ($brand->{success}) {
    print "Brand created with ID: " . $brand->{data}{id} . "\n";
}

# Get a brand by ID
my $fetched = $ccai->brand->get($brand->{data}{id});
print "Brand name: " . $fetched->{data}{legalCompanyName} . "\n";

# List all brands
my $list = $ccai->brand->list();
print "Total brands: " . scalar(@{$list->{data}}) . "\n";

# Update a brand (partial update)
$ccai->brand->update($brand->{data}{id}, {
    street => '456 Oak Avenue',
    city   => 'Los Angeles',
});

# Delete a brand
$ccai->brand->delete($brand->{data}{id});
```

**Entity Types:** `PRIVATE_PROFIT`, `PUBLIC_PROFIT`, `NON_PROFIT`, `GOVERNMENT`, `SOLE_PROPRIETOR`

**Vertical Types:** `AUTOMOTIVE`, `AGRICULTURE`, `BANKING`, `COMMUNICATION`, `CONSTRUCTION`, `EDUCATION`, `ENERGY`, `ENTERTAINMENT`, `GOVERNMENT`, `HEALTHCARE`, `HOSPITALITY`, `INSURANCE`, `LEGAL`, `MANUFACTURING`, `NON_PROFIT`, `PROFESSIONAL`, `REAL_ESTATE`, `RETAIL`, `TECHNOLOGY`, `TRANSPORTATION`

## 8. Campaign Registration

Register and manage campaigns for TCR carrier vetting.

```perl
use lib '.';
use CCAI;
use JSON;

my $ccai = CCAI->new({
    client_id => 'YOUR-CLIENT-ID',
    api_key   => 'API-KEY-TOKEN'
});

# Create a campaign
my $campaign = $ccai->campaign->create({
    brandId          => 1,
    useCase          => 'MIXED',
    subUseCases      => ['CUSTOMER_CARE', 'TWO_FACTOR_AUTHENTICATION', 'ACCOUNT_NOTIFICATION'],
    description      => 'Security codes and support messaging.',
    messageFlow      => 'Users opt-in via signup form at https://example.com/signup',
    hasEmbeddedLinks => JSON::true,
    hasEmbeddedPhone => JSON::false,
    isAgeGated       => JSON::false,
    isDirectLending  => JSON::false,
    optInKeywords    => ['START'],
    optInMessage     => 'Welcome! Reply STOP to cancel.',
    optInProofUrl    => 'https://example.com/opt-in-proof.png',
    helpKeywords     => ['HELP'],
    helpMessage      => 'For HELP email support@example.com.',
    optOutKeywords   => ['STOP'],
    optOutMessage    => 'STOP received. You are unsubscribed.',
    sampleMessages   => [
        'Your code is 554321. Reply STOP to cancel.',
        'Your ticket has been updated. Reply HELP for info.',
    ],
});

if ($campaign->{success}) {
    print "Campaign created with ID: " . $campaign->{data}{id} . "\n";
}

# Get a campaign by ID
my $fetched = $ccai->campaign->get($campaign->{data}{id});

# List all campaigns
my $list = $ccai->campaign->list();
print "Total campaigns: " . scalar(@{$list->{data}}) . "\n";

# Update a campaign (partial update)
$ccai->campaign->update($campaign->{data}{id}, {
    description => 'Updated description.',
});

# Delete a campaign
$ccai->campaign->delete($campaign->{data}{id});
```

**Use Cases:** `TWO_FACTOR_AUTHENTICATION`, `ACCOUNT_NOTIFICATION`, `CUSTOMER_CARE`, `DELIVERY_NOTIFICATION`, `FRAUD_ALERT`, `HIGHER_EDUCATION`, `LOW_VOLUME_MIXED`, `MARKETING`, `MIXED`, `POLLING_VOTING`, `PUBLIC_SERVICE_ANNOUNCEMENT`, `SECURITY_ALERT`

> `MIXED` and `LOW_VOLUME_MIXED` campaigns require 2–3 `subUseCases`.

**Sub-Use Cases:** `TWO_FACTOR_AUTHENTICATION`, `ACCOUNT_NOTIFICATION`, `CUSTOMER_CARE`, `DELIVERY_NOTIFICATION`, `FRAUD_ALERT`, `MARKETING`, `POLLING_VOTING`

## 9. Project Structure

* **lib/ -** Library modules
  * **CCAI.pm -** Main CCAI client class
  * **CCAI/SMS.pm -** SMS service class
  * **CCAI/MMS.pm -** MMS service class
  * **CCAI/Email.pm -** Email service class
  * **CCAI/Webhook.pm -** Webhook service class
* **examples/ -** Example usage scripts
* **t/ -** Test files
* **cpanfile -** Dependency specification

## 10. Development

### Prerequisites

* Perl 5.16.0 or higher
* cpanm or cpan for installing dependencies

### Setup

1. Clone the repository
2. Install dependencies:

```
cpanm --installdeps
```

3. Run examples:

```
\perl examples/sms_example.pl
```

### Testing

Run tests with prove:

```
# Run all tests
prove -l t/

# Run tests with verbose output
prove -lv t/

# Run specific test file
prove -lv t/01-basic.t
```

<br />

## 11. Features

* Object-oriented Perl interface
* Support for sending SMS to multiple recipients
* Support for sending MMS with images
* Support for sending email campaigns
* Support for managing webhooks
* Upload images to S3 with signed URLs
* Support for template variables (firstName, lastName)
* Progress tracking via callbacks
* Comprehensive error handling
* Unit tests
* Modern Perl practices
* Automatic SSL certificate configuration

<br />

## 12. SSL Certificate Handling

The CCAI client automatically configures SSL certificates using the Mozilla::CA module. If you encounter SSL certificate errors:

* Automatic (Recommended): The client handles this automatically when Mozilla::CA is installed
* Manual: Set the environment variable:

```
* export PERL_LWP_SSL_CA_FILE=$(perl -MMozilla::CA -e 'print Mozilla::CA::SSL_ca_file()')
* <br />
```

* System CA: On some systems, you might need:

```
export PERL_LWP_SSL_CA_FILE=/etc/ssl/certs/ca-certificates.crt
```

## 13. Warning Suppression

The CCAI client may show harmless "Content-Length header value was wrong, fixed" warnings from LWP::UserAgent. These warnings don't affect functionality but can be suppressed:

### Method 1: Environment Variable (Recommended)

```
# in your .env file:
CCAI_SUPPRESS_WARNINGS=1
```

### Method 2: Programmatically

```
my $ccai = CCAI->new({
    client_id => $client_id,
    api_key   => $api_key
});

# Suppress warnings after creating the client
$ccai->suppress_lwp_warnings();
```

### Method 3: In Your Script

```
# At the beginning of your script
BEGIN {
    $SIG{__WARN__} = sub {
        my $warning = shift;
        return if $warning =~ /Content-Length header value was wrong, fixed/;
        warn $warning;
    };
}
```

## 14. Error Handling

All methods return a hash reference with the following structure:

```
# Success response
{
    success => 1,
    data    => { ... }  # API response data
}

# Error response
{
    success => 0,
    error   => "Error message"
}
```

## 15. Template Variables

Messages support template variables that are automatically replaced:

* `${firstName}` Fill in with the contact's first name
* `${lastName}` Fill in with the contact's last nam

Example:

```
my $message = "Hello \${firstName} \${lastName}, welcome!";
# For John Doe, becomes: "Hello John Doe, welcome!"
```

<br />

## &#x20;Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-perl).

<br />
