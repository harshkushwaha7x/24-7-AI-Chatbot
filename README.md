# Intelligent Customer Support Agent with LangGraph

An AI-powered customer support workflow built using LangGraph, LangChain, and OpenAI. This project demonstrates how to create an intelligent multi-step support agent that can categorize customer queries, analyze sentiment, generate responses, and escalate critical issues automatically.

## Overview

This tutorial demonstrates how to create an intelligent customer support agent using LangGraph, a powerful tool for building complex language model workflows. The agent is designed to categorize customer queries, analyze sentiment, and provide appropriate responses or escalate issues when necessary.

## Features

- **Query Categorization**: Automatically classifies customer queries into Technical, Billing, or General categories
- **Sentiment Analysis**: Determines the emotional tone of customer queries (Positive, Neutral, or Negative)
- **Automated Response Generation**: Creates appropriate responses based on the query category and sentiment
- **Escalation Workflow**: Automatically escalates queries with negative sentiment to human agents
- **Graph-based Workflow Orchestration**: Utilizes LangGraph to create a flexible and extensible workflow
- **Modular Architecture**: Easy to extend and customize for specific business needs

## Tech Stack

- Python 3.12+
- LangGraph
- LangChain Core
- LangChain OpenAI
- OpenAI API
- python-dotenv
- IPython

## Project Workflow

The application processes customer queries through the following pipeline:

1. **Categorize Query**: Classify the customer query into Technical, Billing, or General
2. **Analyze Sentiment**: Determine if the sentiment is Positive, Neutral, or Negative
3. **Route Dynamically**: Direct the query to the appropriate handler based on sentiment and category
4. **Generate Response**: Create a contextual response or escalate to human agent
5. **Return Result**: Provide the final response to the customer

## Workflow Graph

```text
Start
  │
  ▼
Categorize Query
  │
  ▼
Analyze Sentiment
  │
  ├── Negative ──► Escalate to Human Agent
  │
  ├── Technical ─► Technical Support Handler
  │
  ├── Billing ───► Billing Support Handler
  │
  └── General ───► General Support Handler
       │
       ▼
      End
```

## Installation

### Prerequisites

- Python 3.12 or higher
- OpenAI API key

### Clone the Repository

```bash
git clone https://github.com/harshkushwaha7x/customer-support-agent-langgraph.git
cd customer-support-agent-langgraph
```

### Create Virtual Environment

```bash
python -m venv venv
```

### Activate Virtual Environment

**Windows:**
```bash
venv\Scripts\activate
```

**Mac/Linux:**
```bash
source venv/bin/activate
```

### Install Dependencies

```bash
pip install langgraph langchain-core langchain-openai python-dotenv ipython
```

## Configuration

### Environment Variables

Create a `.env` file in the root directory:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

Replace `your_openai_api_key_here` with your actual OpenAI API key.

## Project Structure

```text
.
├── customer_support_agent_langgraph.ipynb
├── README.md
└── .env
```

## Core Components

### 1. State Management

The workflow uses a `TypedDict` state structure to store:

- `query`: The customer's question or issue
- `category`: Classification of the query (Technical, Billing, General)
- `sentiment`: Emotional tone (Positive, Neutral, Negative)
- `response`: Generated response or escalation message

### 2. Query Categorization

Customer queries are classified into three categories:

- **Technical**: Issues related to product functionality, bugs, or technical problems
- **Billing**: Questions about payments, invoices, subscriptions, or charges
- **General**: General inquiries about business hours, policies, or other information

### 3. Sentiment Analysis

The system detects the emotional tone of customer queries:

- **Positive**: Customer is satisfied or expressing gratitude
- **Neutral**: Factual inquiry without strong emotion
- **Negative**: Customer is frustrated, angry, or dissatisfied

### 4. Dynamic Routing

Queries are routed automatically based on sentiment and category:

- Negative sentiment queries are immediately escalated to human agents
- Other queries are routed to specialized handlers based on their category

### 5. Response Handlers

- **Technical Handler**: Provides technical support responses
- **Billing Handler**: Addresses billing and payment inquiries
- **General Handler**: Handles general information requests
- **Escalation Handler**: Routes critical issues to human agents

## Usage

### Running the Notebook

1. Open the Jupyter notebook:

```bash
jupyter notebook customer_support_agent_langgraph.ipynb
```

2. Run all cells to initialize the workflow

3. Use the `run_customer_support()` function to process queries

### Example Queries

```python
# Technical query with negative sentiment (escalated)
query = "My internet connection keeps dropping. Can you help?"
result = run_customer_support(query)
print(f"Category: {result['category']}")
print(f"Sentiment: {result['sentiment']}")
print(f"Response: {result['response']}")

# Technical query with neutral sentiment
query = "I need help talking to chatGPT"
result = run_customer_support(query)

# Billing query
query = "where can i find my receipt?"
result = run_customer_support(query)

# General query
query = "What are your business hours?"
result = run_customer_support(query)
```

### Example Output

```python
{
    'category': 'Billing',
    'sentiment': 'Negative',
    'response': 'This query has been escalated to a human agent due to its negative sentiment.'
}
```

## Use Cases

- AI-powered customer support systems
- Helpdesk automation and ticket routing
- Intelligent chatbot backends
- SaaS support automation
- Multi-channel support orchestration
- Customer service quality assurance

## Key Concepts Demonstrated

This project showcases several important concepts:

- **LangGraph Workflow Creation**: Building complex, multi-step AI workflows
- **Conditional Routing**: Dynamic decision-making based on query attributes
- **State Management**: Maintaining context throughout the workflow
- **Prompt Engineering**: Crafting effective prompts for different tasks
- **AI-Powered Automation**: Reducing manual workload in customer support

## Future Improvements

- Multi-language support for international customers
- Database integration for customer history and context
- Memory-enabled conversations for follow-up queries
- Vector database support for knowledge base retrieval
- Human-in-the-loop review system for quality assurance
- Deployment using FastAPI or Streamlit for production use
- Integration with ticketing systems (Zendesk, Freshdesk, etc.)
- Analytics dashboard for monitoring agent performance
- A/B testing framework for response optimization

## Learning Outcomes

By exploring this project, you will learn:

- How to build graph-based AI workflows with LangGraph
- Implementing conditional routing in AI applications
- Managing state in multi-step AI pipelines
- Effective prompt engineering techniques
- Creating production-ready AI automation systems
- Integrating OpenAI models with custom business logic

## Motivation

In today's fast-paced business environment, efficient and accurate customer support is crucial. Automating the initial stages of customer interaction can significantly reduce response times and improve overall customer satisfaction. This project aims to showcase how advanced language models and graph-based workflows can be combined to create a sophisticated support system that can handle a variety of customer inquiries.

## Conclusion

This tutorial demonstrates the power and flexibility of LangGraph in creating complex, AI-driven workflows. By combining natural language processing capabilities with a structured graph-based approach, we have created a customer support agent that can efficiently handle a wide range of queries. This system can be further extended and customized to meet specific business needs, potentially integrating with existing customer support tools and databases for even more sophisticated interactions.

The approach showcased here has broad applications beyond customer support, illustrating how language models can be effectively orchestrated to solve complex, multi-step problems in various domains.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is open source and available under the MIT License.

## Author

Developed by Harsh Kushwaha

GitHub: [harshkushwaha7x](https://github.com/harshkushwaha7x)

## Acknowledgments

- Built with LangGraph and LangChain
- Powered by OpenAI's language models
- Inspired by real-world customer support challenges
