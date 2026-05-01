# Intelligent Customer Support Agent with LangGraph

An AI-powered customer support workflow built using **LangGraph**, **LangChain**, and **OpenAI**.  
This project demonstrates how to create an intelligent multi-step support agent that can categorize customer queries, analyze sentiment, generate responses, and escalate critical issues automatically.

## Features

- Query categorization
  - Technical
  - Billing
  - General

- Sentiment analysis
  - Positive
  - Neutral
  - Negative

- Automated response generation

- Escalation workflow for negative sentiment

- Graph-based workflow orchestration using LangGraph

- Modular and extensible architecture

---

## Tech Stack

- Python
- LangGraph
- LangChain
- OpenAI API
- dotenv

---

## Project Workflow

The application processes customer queries through the following pipeline:

1. Categorize the customer query
2. Analyze customer sentiment
3. Route the query dynamically
4. Generate a response
5. Escalate if sentiment is negative

---

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
```

---

## Installation

### Clone the repository

```bash
git clone https://github.com/your-username/intelligent-customer-support-agent.git](https://github.com/harshkushwaha7x/24-7-AI-Chatbot.git
cd intelligent-customer-support-agent
```

### Create virtual environment

```bash
python -m venv venv
```

### Activate virtual environment

#### Windows

```bash
venv\Scripts\activate
```

#### Mac/Linux

```bash
source venv/bin/activate
```

### Install dependencies

```bash
pip install -r requirements.txt
```

Or install manually:

```bash
pip install langgraph langchain-core langchain-openai python-dotenv ipython
```

---

## Environment Variables

Create a `.env` file in the root directory:

```env
OPENAI_API_KEY=your_openai_api_key
```

---

## Project Structure

```text
├── customer_support_agent.ipynb
├── README.md
├── requirements.txt
└── .env
```

---

## Core Components

### 1. State Management

The workflow uses a `TypedDict` state structure to store:

- Query
- Category
- Sentiment
- Response

### 2. Query Categorization

Customer queries are classified into:

- Technical
- Billing
- General

### 3. Sentiment Analysis

The system detects emotional tone:

- Positive
- Neutral
- Negative

### 4. Dynamic Routing

Queries are routed automatically based on sentiment and category.

### 5. Escalation Mechanism

Negative sentiment queries are escalated to a human support agent.

---

## Example Query

```python
query = {
    "query": "I was charged twice for my subscription."
}

result = app.invoke(query)

print(result)
```

### Example Output

```python
{
    'query': 'I was charged twice for my subscription.',
    'category': 'Billing',
    'sentiment': 'Negative',
    'response': 'This query has been escalated to a human agent due to its negative sentiment.'
}
```

---

## Use Cases

- AI customer support systems
- Helpdesk automation
- Intelligent ticket routing
- SaaS support automation
- Workflow orchestration with LLMs

---

## Future Improvements

- Multi-language support
- Database integration
- Memory-enabled conversations
- Vector database support
- Human-in-the-loop review system
- Deployment using FastAPI or Streamlit

---

## Learning Outcomes

This project demonstrates:

- LangGraph workflow creation
- Conditional routing
- State management in AI pipelines
- Prompt engineering
- AI-powered automation systems

---

## Author

Developed by Harsh Kushwaha
GitHub: https://github.com/harshkushwaha7x
