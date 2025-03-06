---
title: Flows
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fwww.youtube.com%2Fembed%2FGRQAq_4MzUg%3Ffeature%3Doembed&display_name=YouTube&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DGRQAq_4MzUg&image=https%3A%2F%2Fi.ytimg.com%2Fvi%2FGRQAq_4MzUg%2Fhqdefault.jpg&key=7788cb384c9f4d5dbbdbeffd9fe4b92f&type=text%2Fhtml&schema=youtube\" width=\"854\" height=\"480\" scrolling=\"no\" title=\"YouTube embed\" frameborder=\"0\" allow=\"autoplay; fullscreen; encrypted-media; picture-in-picture;\" allowfullscreen=\"true\"></iframe>",
  "url": "https://www.youtube.com/watch?v=GRQAq_4MzUg",
  "title": "CloudContactAI Flow Tutorial",
  "favicon": "https://www.google.com/favicon.ico",
  "image": "https://i.ytimg.com/vi/GRQAq_4MzUg/hqdefault.jpg",
  "provider": "https://www.youtube.com/",
  "href": "https://www.youtube.com/watch?v=GRQAq_4MzUg",
  "typeOfEmbed": "youtube"
}
[/block]


<br />

Flows are automated campaigns that trigger multiple messages to contacts based on time and contact feedback.  All users have access to the flows feature whether they are a paid user, or are still using the free trial.  Flows can be found on the sidebar menu.

There are options to build either an SMS flow or an email flow.  Both UIs are visually similar and work the same for their respective medium types.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ea30112-ccai_flow_page.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


When opening a new flow, the user will be provided the option to build a flow from a blank slate or to use a pre-built template.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/22d83fa-ccai_flow_template.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


The flow builder will provide an open board to build the flow vertically and horizontally, or build additional logic flows parallel.  The user can click and drag around the screen to view other parts of their flow as much as they need. 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cf89318-ccai_flow_message_page.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


The menu on the side of the window provides new nodes for the user to click and drag onto the field as they need.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f85daef-ccai_flow_node_menu.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


Whenever the user clicks on a node, it will provide a smaller menu with all the same node options, but with additional options with the node specifically.  Clicking and dragging the arrow will add a new connection to any neighboring nodes.  The paintbrush will change the color for visual aids.  The trash can will completely remove the node from the screen.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cf7c07d-ccai_flow_mini_menu.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


At the top right of the window is a minimap that can toggle with a click.  Either by clicking and dragging on the minimap or the window itself, the user can move the map around to center the screen on other parts of the flow.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/479d7da-ccai_flow_minimap.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


<br />

<br />

## Node Types

### Start

![](<>)

The start node is self-explanatory.  It is required for the logic to initiate and deliver the flow.

<br />

### Wait for SMS

![](<>)

The Wait for SMS node will pause the flow until there is a response from the contact.

<br />

### End

![](<>)

The end node is also self-explanatory and is also required for the flow to stop.

<br />

### Add Delay

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3c1930c-ccai_flow_delay_selection.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


The Add Delay node will pause the flow on a timer.  The user can adjust how long the delay lasts from seconds up to years.

<br />

### Condition Trigger

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7ca8443-ccai_flow_condition_default.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


The condition trigger is an automated response with logic that ties into the contact's last response or lack thereof.  The 'default flow' tick will disable the condition settings and establish that route as the action to take if the user does not respond.

Toggling off the condition will allow the user to set the condition and the subsequent value.  This value can either be alphabetical or numerical.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a99d66b-ccai_flow_condition_options.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


<br />

### Send Message

The send message node is what the flow will send out after the flow has reached that phase.  Clicking on the node will provide a box at the bottom to provide a message to send.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f1daa13-ccai_flow_message_node.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


<br />

## Flow Completion and Use

At the top of the flow window is a blue hotbar.  On the left is the option to change the flow's name and description for categorization purposes.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f9f1fcb-ccai_flow_name.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c0e4810-ccai_flow_save.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8df4c61-ccai_flow_save_flow.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


After saving, the user will be directed back to the flow menu.  Here, they can see their newly added flow.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/540990c-ccai_flow_menu.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


Using a flow is a matter of opening the campaign builder of the respective flow type and setting the campaign to 'workflow.'  The message builder will be grayed out because the messages are set to a predetermined path.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4297958-ccai_sms_flow.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fwww.youtube.com%2Fembed%2FGRQAq_4MzUg%3Ffeature%3Doembed&display_name=YouTube&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DGRQAq_4MzUg&image=https%3A%2F%2Fi.ytimg.com%2Fvi%2FGRQAq_4MzUg%2Fhqdefault.jpg&key=7788cb384c9f4d5dbbdbeffd9fe4b92f&type=text%2Fhtml&schema=youtube\" width=\"854\" height=\"480\" scrolling=\"no\" title=\"YouTube embed\" frameborder=\"0\" allow=\"autoplay; fullscreen; encrypted-media; picture-in-picture;\" allowfullscreen=\"true\"></iframe>",
  "url": "https://www.youtube.com/watch?v=GRQAq_4MzUg",
  "title": "CloudContactAI Flow Tutorial",
  "favicon": "https://www.google.com/favicon.ico",
  "image": "https://i.ytimg.com/vi/GRQAq_4MzUg/hqdefault.jpg",
  "provider": "https://www.youtube.com/",
  "href": "https://www.youtube.com/watch?v=GRQAq_4MzUg",
  "typeOfEmbed": "youtube"
}
[/block]