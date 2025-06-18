---
title: SMS and Email Workflows
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: SMS and EMail Workflows with CloudContactAI
  description: SMS and EMail Workflows are supported by CloudContactAI's UI and API
  image: >-
    https://files.readme.io/edc575a9cc903999b7552c1bbc07a92c0441d7d1ee32d03d5859958fff744333-Group_84_1.png
  keywords:
    - sms
    - email
    - workflow
    - api
    - ui
    - cloudcontactai
  robots: index
next:
  description: ''
---
<Embed url="https://www.youtube.com/watch?v=GRQAq_4MzUg" title="CloudContactAI Flow Tutorial" favicon="https://www.google.com/favicon.ico" image="https://i.ytimg.com/vi/GRQAq_4MzUg/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/watch?v=GRQAq_4MzUg" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FGRQAq_4MzUg%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DGRQAq_4MzUg%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FGRQAq_4MzUg%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

<br />

Flows are automated campaigns that trigger multiple messages to contacts based on time and contact feedback.  All users have access to the flows feature whether they are a paid user, or are still using the free trial.  Flows can be found on the sidebar menu.

There are options to build either an SMS flow or an email flow.  Both UIs are visually similar and work the same for their respective medium types.

<Image align="center" src="https://files.readme.io/ea30112-ccai_flow_page.png" />

When opening a new flow, the user will be provided the option to build a flow from a blank slate or to use a pre-built template.

<Image align="center" src="https://files.readme.io/22d83fa-ccai_flow_template.png" />

The flow builder will provide an open board to build the flow vertically and horizontally, or build additional logic flows parallel.  The user can click and drag around the screen to view other parts of their flow as much as they need. 

<Image align="center" src="https://files.readme.io/cf89318-ccai_flow_message_page.png" />

The menu on the side of the window provides new nodes for the user to click and drag onto the field as they need.

<Image align="center" src="https://files.readme.io/f85daef-ccai_flow_node_menu.png" />

Whenever the user clicks on a node, it will provide a smaller menu with all the same node options, but with additional options with the node specifically.  Clicking and dragging the arrow will add a new connection to any neighboring nodes.  The paintbrush will change the color for visual aids.  The trash can will completely remove the node from the screen.

<Image align="center" src="https://files.readme.io/cf7c07d-ccai_flow_mini_menu.png" />

At the top right of the window is a minimap that can toggle with a click.  Either by clicking and dragging on the minimap or the window itself, the user can move the map around to center the screen on other parts of the flow.

<Image align="center" src="https://files.readme.io/479d7da-ccai_flow_minimap.png" />

<br />

<br />

## Node Types

### Start

![]()

The start node is self-explanatory.  It is required for the logic to initiate and deliver the flow.

<br />

### Wait for SMS

![]()

The Wait for SMS node will pause the flow until there is a response from the contact.

<br />

### End

![]()

The end node is also self-explanatory and is also required for the flow to stop.

<br />

### Add Delay

<Image align="center" src="https://files.readme.io/3c1930c-ccai_flow_delay_selection.png" />

The Add Delay node will pause the flow on a timer.  The user can adjust how long the delay lasts from seconds up to years.

<br />

### Condition Trigger

<Image align="center" src="https://files.readme.io/7ca8443-ccai_flow_condition_default.png" />

The condition trigger is an automated response with logic that ties into the contact's last response or lack thereof.  The 'default flow' tick will disable the condition settings and establish that route as the action to take if the user does not respond.

Toggling off the condition will allow the user to set the condition and the subsequent value.  This value can either be alphabetical or numerical.

<Image align="center" src="https://files.readme.io/a99d66b-ccai_flow_condition_options.png" />

<br />

### Send Message

The send message node is what the flow will send out after the flow has reached that phase.  Clicking on the node will provide a box at the bottom to provide a message to send.

<Image align="center" src="https://files.readme.io/f1daa13-ccai_flow_message_node.png" />

<br />

## Flow Completion and Use

At the top of the flow window is a blue hotbar.  On the left is the option to change the flow's name and description for categorization purposes.

<Image align="center" src="https://files.readme.io/f9f1fcb-ccai_flow_name.png" />

<Image align="center" src="https://files.readme.io/c0e4810-ccai_flow_save.png" />

<Image align="center" src="https://files.readme.io/8df4c61-ccai_flow_save_flow.png" />

After saving, the user will be directed back to the flow menu.  Here, they can see their newly added flow.

<Image align="center" src="https://files.readme.io/540990c-ccai_flow_menu.png" />

Using a flow is a matter of opening the campaign builder of the respective flow type and setting the campaign to 'workflow.'  The message builder will be grayed out because the messages are set to a predetermined path.

<Image align="center" src="https://files.readme.io/4297958-ccai_sms_flow.png" />

<Embed url="https://www.youtube.com/watch?v=GRQAq_4MzUg" title="CloudContactAI Flow Tutorial" favicon="https://www.google.com/favicon.ico" image="https://i.ytimg.com/vi/GRQAq_4MzUg/hqdefault.jpg" provider="youtube.com" href="https://www.youtube.com/watch?v=GRQAq_4MzUg" typeOfEmbed="youtube" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FGRQAq_4MzUg%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DGRQAq_4MzUg%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FGRQAq_4MzUg%252Fhqdefault.jpg%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />