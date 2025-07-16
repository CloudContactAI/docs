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
Learn how to send your first SMS using the CCAI Perl SDK

## Prerequisites

To get the most out of this guide, you'll need to:

* Sign up for a CCAI Paid Plan
* Create an API Key
* Get your Client ID
* Watch this video if you need help.

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=CXTrFkXnmXs" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FCXTrFkXnmXs%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DCXTrFkXnmXs%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FCXTrFkXnmXs%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=CXTrFkXnmXs" providerUrl="https://www.youtube.com/" providerName="YouTube" />

## 1. Install

Get the CCAI Perl SDK

```text
git clone https://github.com/cloudcontactai/ccai-perl.git
cd ccai-perl
cpanm --installdeps .

# Verify SSL configuration
perl verify_ssl.pl

```

## 2. Send SMS message

```perl
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
        first_name => "John",
        last_name  => "Doe",
        phone      => "+15551234567"
    },
    {
        first_name => "Jane",
        last_name  => "Smith", 
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
    "Hi \${first_name}, thanks for your interest!",
    "Single Message Test"
);

if ($single_response->{success}) {
    print "Single SMS sent successfully!\n";
} else {
    print "Error: " . $single_response->{error} . "\n";
    }
    
#Update YOUR-CLIENT-ID and API-KEY-TOKEN in sms_example.sh

# Test with example
./runs_sms_example.pl

or 

perl -Ilib examples/sms_example.pl
```

## 3. Send MMS Message

```perl
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
        first_name => 'John',
        last_name  => 'Doe',
        phone      => '+15551234567'
    });
    
    # Send MMS with image in one step
    my $response = $ccai->mms->send_with_image(
        $image_path,
        $content_type,
        \@accounts,
        "Hello \${first_name}, check out this image!",
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

<br />

## 4. Try it yourself

See the full source code [here](https://github.com/CloudContactAI/ccai-perl).