---
title: AI Agents
excerpt: CloudContactAI Semi-Agentic Workflow Solution
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: how-to-configure-your-cloudcontactai-agent
      title: How to configure your CloudContactAI Agent
---
CloudContactAI leverages advanced AI technologies to create intelligent agents that can respond to SMS text messages efficiently and accurately. By integrating [OpenAI](https://openai.com), [DSPy](https://dspy-docs.vercel.app/intro/), and [FAISS](https://ai.meta.com/tools/faiss/), the solution enhances customer interactions through automated, context-aware responses.

**Key Components**

1. OpenAI: Utilizes powerful language models to understand and generate human-like text. This enables the AI agents to comprehend customer inquiries and provide relevant responses.
2. DSPy: A Python library that facilitates the deployment and management of AI models. It helps in orchestrating the interaction between OpenAI's language models and other components of the system.
3. FAISS (Facebook AI Similarity Search): A vector database used for retrieval-augmented generation. It stores and retrieves relevant information quickly, enhancing the AI's ability to provide accurate and contextually appropriate responses.

**Workflow**

1. Message Reception: When a customer sends an SMS to an inbound phone number, CloudContactAI captures the message and the entire communication stream to the AI agent.
2. Information Retrieval: Using FAISS, the system retrieves relevant information from a pre-built knowledge base for your account. This step ensures that the AI agent has access to the most pertinent data to formulate a response.
3. Response Generation: The AI agent powered by OpenAI, with the help of DSPy, generates a response based on the retrieved information and the initial customer query. This response is crafted to be accurate, relevant, and contextually appropriate.
4. Message Delivery: The generated response is sent back to the customer via SMS, ensuring a seamless and efficient communication experience.

**Benefits**  
•  Enhanced Customer Experience: Customers receive quick and accurate responses to their inquiries, improving satisfaction and engagement.

•  Scalability: The solution can handle a large volume of messages simultaneously, making it suitable for businesses of all sizes.

•  Efficiency: Automating responses reduces the need for human intervention, allowing customer service teams to focus on more complex issues.

•  Contextual Accuracy: The use of FAISS for retrieval-augmented generation ensures that responses are not only relevant but also contextually accurate, enhancing the overall quality of interactions.

By integrating OpenAI, DSPy, and FAISS, CloudContactAI provides a robust solution for automating SMS responses, making customer communication more efficient and effective

<br />

<br />

# Implementation

AI Agents have their own tabs under the SMS and Email categories.  Both will be empty and require the user to name a new both with a general description of how the bot will act.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/950b37c6b96e0f53f68e23c6b71d0c9bca02ab1b6540b07b2c71ad31fcec3c35-Screenshot_2024-12-19_111615.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


The 'Create AI Agent' button will open a window requiring a name and a bot description.  Any data, including links, needed for desired bot behavior will need to be inserted into this category.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b96fb3ac2469299adbc46617828721dfe256bbb0df658006b134b65509df4ee0-Screenshot_2024-12-19_111632.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


Even after a bot is created, the chatbot can have its name or parameters altered, or be deleted.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/734bb2ff0ec76ddbe1cdf38c1609e4c35bd7d89bc79b9c67aceb023f124f6695-Screenshot_2024-12-19_112546.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


When you have a personal chatbot built or you are interested in one of the more generic bots, go down to the settings tab and select the last option for general settings.  The toggle for the AI chatbot functionality will be at the bottom.  If you want to stop using the chatbot function, simply untoggle the box.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/25a9cd02024063d94986d78e0690be91e9bef229261d93a915d0e5e857d709aa-Screenshot_2024-12-19_114454.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


Toggling this option will open a dropdown with the generic bot personalities.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/98920213f07250a3d911d73b8bbc551e54c78e0dc9c9608d934fe50bbeb417a2-Screenshot_2024-12-19_111702.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


If you want to select any chatbots you made, select the 'Custom Agent' option.  This will open a second dropdown showing any chatbots on your account.  If you have no custom chatbots made, this dropdown will be replaced by a button prompting the user to build a chatbot.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/994bff40173438e2895f38dd6255563f06c348cb72c3cd4158c5f9dbee19e612-Screenshot_2024-12-19_112616.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


After selecting your chatbot of choice, click the 'Save' button.  The bot is now configured to your account and will respond to contact inquiries. 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9978c825b73e41a4caac76c7ed2e00cb49ed4abebf6d67f12f8fafd5a1a169a9-Screenshot_2024-12-19_112904.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]