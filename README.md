# Customer Support Agent with LangGraph

A production-ready customer support workflow built with LangGraph, LangChain, and OpenAI. This project demonstrates how to build an intelligent multi-step support agent that categorizes customer queries, analyzes sentiment, generates contextual responses, and escalates critical issues automatically.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Technical Details](#technical-details)
- [Use Cases](#use-cases)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [Author](#author)

## Overview

This project showcases how to create an intelligent customer support agent using LangGraph for workflow orchestration. The agent processes customer queries through a structured pipeline that includes categorization, sentiment analysis, and intelligent routing to appropriate response handlers.

## Features

- **Query Categorization**: Automatically classifies customer queries into Technical, Billing, or General categories
- **Sentiment Analysis**: Determines the emotional tone of customer queries (Positive, Neutral, or Negative)
- **Automated Response Generation**: Creates appropriate responses based on the query category and sentiment
- **Escalation Workflow**: Automatically escalates queries with negative sentiment to human agents
- **Graph-based Workflow Orchestration**: Utilizes LangGraph to create a flexible and extensible workflow
- **Modular Architecture**: Easy to extend and customize for specific business needs

### Key Capabilities

- Automatic query categorization (Technical, Billing, General)
- Real-time sentiment analysis (Positive, Neutral, Negative)
- Context-aware response generation
- Intelligent escalation for negative sentiment queries
- Graph-based workflow with conditional routing
- Extensible and modular architecture

### Built With

- **Python** - Core programming language
- **LangGraph** - Workflow orchestration framework
- **LangChain** - LLM application framework
- **OpenAI API** - Language model provider
- **Jupyter Notebook** - Interactive development environment

## Architecture

### Workflow Pipeline

The agent processes queries through a five-stage pipeline:

1. **Entry Point** - Receives customer query
2. **Categorization** - Classifies query type (Technical/Billing/General)
3. **Sentiment Analysis** - Evaluates emotional tone (Positive/Neutral/Negative)
4. **Conditional Routing** - Directs to appropriate handler based on sentiment and category
5. **Response Generation** - Produces contextual response or escalates to human agent

### State Management

The workflow maintains state using a `TypedDict` structure:

```python
class State(TypedDict):
    query: str       # Customer's original query
    category: str    # Classified category
    sentiment: str   # Detected sentiment
    response: str    # Generated response
```

### Routing Logic

```
                    ┌─────────────┐
                    │   START     │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │ Categorize  │
                    └──────┬──────┘
                           │
                    ┌──────▼──────────┐
                    │ Analyze         │
                    │ Sentiment       │
                    └──────┬──────────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
         Negative      Technical    Billing/General
              │            │            │
              ▼            ▼            ▼
        ┌─────────┐  ┌──────────┐  ┌──────────┐
        │Escalate │  │Technical │  │ Billing/ │
        │to Human │  │ Handler  │  │ General  │
        └────┬────┘  └────┬─────┘  └────┬─────┘
             │            │             │
             └────────────┴─────────────┘
                          │
                    ┌─────▼─────┐
                    │    END    │
                    └───────────┘
```

## Installation

### Prerequisites

- Python 3.8 or higher
- pip package manager
- OpenAI API key ([Get one here](https://platform.openai.com/api-keys))

### Setup Instructions

1. **Clone the repository**

```bash
git clone https://github.com/harshkushwaha7x/customer-support-agent-langgraph.git
cd customer-support-agent-langgraph
```

2. **Create and activate virtual environment**

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

3. **Install required packages**

```bash
pip install langgraph langchain-core langchain-openai python-dotenv ipython jupyter
```

**Package versions used:**
- `langgraph` - Latest stable
- `langchain-core` - Latest stable
- `langchain-openai` - Latest stable
- `python-dotenv` - For environment variable management
- `ipython` - Enhanced Python shell
- `jupyter` - Notebook interface

## Configuration

Create a `.env` file in the project root directory:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

**Security Note:** Never commit your `.env` file to version control. Add it to `.gitignore`.

## Technical Details

### Node Functions

The workflow consists of six specialized node functions:

1. **`categorize(state)`** - Classifies queries into Technical, Billing, or General
2. **`analyze_sentiment(state)`** - Determines sentiment as Positive, Neutral, or Negative
3. **`handle_technical(state)`** - Generates technical support responses
4. **`handle_billing(state)`** - Generates billing support responses
5. **`handle_general(state)`** - Generates general information responses
6. **`escalate(state)`** - Routes to human agent for negative sentiment queries

### Routing Function

```python
def route_query(state: State) -> str:
    """Route the query based on its sentiment and category."""
    if state["sentiment"] == "Negative":
        return "escalate"
    elif state["category"] == "Technical":
        return "handle_technical"
    elif state["category"] == "Billing":
        return "handle_billing"
    else:
        return "handle_general"
```

### Model Configuration

- **Model**: OpenAI ChatGPT (via `ChatOpenAI`)
- **Temperature**: 0 (deterministic responses for consistency)
- **Prompt Engineering**: Task-specific prompts for each node function

### Graph Structure

The workflow uses LangGraph's `StateGraph` with:
- **Nodes**: Processing functions for each stage
- **Edges**: Sequential connections between nodes
- **Conditional Edges**: Dynamic routing based on state
- **Entry Point**: `categorize` node
- **End Points**: All handler and escalation nodes

## Project Structure

```
customer-support-agent-langgraph/
│
├── customer_support_agent_langgraph.ipynb    # Main notebook with implementation
├── README.md                                  # Project documentation
├── .env                                       # Environment variables (create this)
└── .gitignore                                 # Git ignore file (recommended)
```

## Usage

### Running the Notebook

1. **Start Jupyter Notebook**

```bash
jupyter notebook
```

2. **Open the notebook**

Navigate to `customer_support_agent_langgraph.ipynb` in your browser

3. **Execute cells sequentially**

Run all cells from top to bottom to:
- Install dependencies (if needed)
- Import libraries
- Define state structure
- Create node functions
- Build and compile the workflow graph
- Test the agent

### Using the Agent

The main function to process queries is `run_customer_support()`:

```python
def run_customer_support(query: str) -> Dict[str, str]:
    """
    Process a customer query through the LangGraph workflow.
    
    Args:
        query (str): The customer's query
        
    Returns:
        Dict[str, str]: Dictionary containing category, sentiment, and response
    """
    results = app.invoke({"query": query})
    return {
        "category": results["category"],
        "sentiment": results["sentiment"],
        "response": results["response"]
    }
```

### Example Queries

**Example 1: Technical Issue with Negative Sentiment (Escalated)**

```python
query = "My internet connection keeps dropping. Can you help?"
result = run_customer_support(query)

print(f"Query: {query}")
print(f"Category: {result['category']}")      # Output: Technical
print(f"Sentiment: {result['sentiment']}")    # Output: Negative
print(f"Response: {result['response']}")      
# Output: This query has been escalated to a human agent due to its negative sentiment.
```

**Example 2: Technical Query with Neutral Sentiment**

```python
query = "I need help talking to chatGPT"
result = run_customer_support(query)

print(f"Category: {result['category']}")      # Output: Technical
print(f"Sentiment: {result['sentiment']}")    # Output: Neutral
print(f"Response: {result['response']}")      
# Output: [Detailed technical support response]
```

**Example 3: Billing Query**

```python
query = "where can i find my receipt?"
result = run_customer_support(query)

print(f"Category: {result['category']}")      # Output: Billing
print(f"Sentiment: {result['sentiment']}")    # Output: Neutral
print(f"Response: {result['response']}")      
# Output: [Billing support response with receipt location instructions]
```

**Example 4: General Information Query**

```python
query = "What are your business hours?"
result = run_customer_support(query)

print(f"Category: {result['category']}")      # Output: General
print(f"Sentiment: {result['sentiment']}")    # Output: Neutral
print(f"Response: {result['response']}")      
# Output: [General information response]
```

## Use Cases

This implementation is suitable for:

- **Customer Support Automation** - First-line response to common queries
- **Helpdesk Triage** - Automatic categorization and routing of support tickets
- **Chatbot Backend** - Intelligent conversation flow management
- **SaaS Support Systems** - Scalable support for software products
- **E-commerce Support** - Order, billing, and product inquiry handling
- **Service Desk Operations** - IT support ticket classification and routing

## Future Enhancements

Potential improvements and extensions:

- **Multi-language Support** - Detect and respond in customer's language
- **Conversation Memory** - Maintain context across multiple interactions
- **Knowledge Base Integration** - RAG implementation with vector databases
- **Custom Training** - Fine-tune models on company-specific data
- **Analytics Dashboard** - Track metrics, response times, and satisfaction
- **CRM Integration** - Connect with Salesforce, HubSpot, or Zendesk
- **API Deployment** - FastAPI or Flask REST API for production use
- **Web Interface** - Streamlit or Gradio frontend for testing
- **Multi-channel Support** - Email, Slack, Teams integration
- **A/B Testing** - Compare different prompts and routing strategies

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
