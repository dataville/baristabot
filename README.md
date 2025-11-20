# BaristaBot: AI-Powered Cafe Ordering System

A conversational AI ordering system built with LangGraph and Google Gemini that implements semantic menu search, order state management, and automated response quality control.

## Overview

This project implements a multi-agent conversational system for cafe ordering. The system uses vector-based semantic search for menu retrieval, maintains stateful order information throughout the conversation, and evaluates AI responses before presenting them to users.

## Technical Implementation

### Core Architecture

- **LangGraph**: State graph implementation for conversation flow control
- **Google Gemini (gemini-1.5-flash)**: Language model for natural language understanding and generation
- **FAISS**: Vector database for semantic menu search with cosine similarity
- **LangChain**: Framework integration and tooling

### Key Components

**Vector-Based Menu Search**
- FAISS vector store with GoogleGenerativeAI embeddings
- Semantic search supporting natural language queries
- k=4 nearest neighbor retrieval for relevant menu items

**Order State Management**
- Persistent order state across conversation turns
- Operations: add_to_order, confirm_order, get_order, clear_order, place_order
- Explicit confirmation required before finalizing orders

**Response Quality Control**
- Automated evaluation of AI responses before delivery
- Correction system for responses not meeting quality standards
- Verification against menu constraints and clarity requirements

**Conversation Flow**
- Five-node graph: chatbot, human, tools, ordering, evaluator
- Dynamic routing based on tool calls and message content
- Recursion limit of 100 for extended conversations

## Attribution

Based on the [5-Day Gen AI Intensive Course](https://www.kaggle.com/learn-guide/5-day-genai) original code from [Day 3 - Building an Agent with LangGraph](https://www.kaggle.com/code/markishere/day-3-building-an-agent-with-langgraph/).

**Course Developers**: Addison Howard, Brenda Flynn, Myles O'Neill, Nate, Polong Lin

**Competition**: [Gen AI Intensive Course Capstone 2025Q1](https://kaggle.com/competitions/gen-ai-intensive-course-capstone-2025q1)

## Enhancements Over Original

1. **Vector Database Integration**: Replaced hardcoded menu with FAISS vector store for scalable, semantic menu search
2. **RAG Implementation**: Dynamic retrieval of menu information based on query context
3. **Quality Evaluation System**: LLM-based response validation and correction before user presentation
4. **Enhanced Tool Organization**: Separation of informational tools (menu search) from state-modifying tools (order management)

## Dependencies

```
langgraph==0.3.21
langchain-google-genai==2.1.2
langgraph-prebuilt==0.1.7
langchain_community
faiss-cpu
```

## Configuration

Requires `GOOGLE_API_KEY` environment variable for Gemini API access. In Kaggle environments, this should be stored as a Kaggle secret.

## Usage

The system initiates with a welcome message and enters a conversation loop. Users can:
- Search menu items using natural language
- Add items to order with specifications (milk type, sweetness, temperature)
- View current order
- Confirm and place orders
- Exit conversation with 'q' command

## Technical Notes

**Vector Search Implementation**
- Embedding model: models/embedding-001
- Distance metric: Cosine similarity
- Retrieval configuration: Top 4 results

**State Management**
- TypedDict-based state with annotated message history
- Order state persists across graph invocations
- Tool call metadata preserved during evaluation corrections

**Graph Compilation**
- Conditional edges for dynamic routing
- Tool execution loops back to chatbot node
- Evaluator positioned between chatbot and routing logic

## License

Apache License 2.0
