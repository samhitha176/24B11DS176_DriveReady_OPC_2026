# Day 5 – Memory and RAG: TravelEase AI Agent

## Overview

Day 5 focuses on building an AI agent that can remember previous conversations and retrieve relevant information from a custom knowledge base using Retrieval-Augmented Generation (RAG).

As an extension of the Day 4 TravelEase AI Booking Assistant, this implementation integrates ChromaDB for semantic search and LangGraph's InMemorySaver for conversation memory.

The agent can answer travel-related questions, retrieve package information, maintain customer conversation context, and handle questions about unsupported destinations.

## Objectives

- Understand Retrieval-Augmented Generation (RAG).
- Learn how vector databases store and retrieve information.
- Implement semantic search using ChromaDB.
- Integrate RAG with a LangChain AI agent.
- Implement conversation memory using InMemorySaver.
- Maintain separate conversations using thread IDs.
- Test the agent with different customer queries.

## Technologies Used

- Python
- LangChain
- LangGraph
- Groq LLM
- ChromaDB
- Google Colab
- Google Sheets
- Pydantic

## Implementation

### 1. Knowledge Base Creation

Created a custom TravelEase knowledge base containing information about:

- Available travel packages.
- Package pricing and duration.
- Supported destinations.
- Booking requirements.
- 48-hour advance booking policy.
- Booking confirmation and availability policies.

### 2. Vector Database – ChromaDB

Used ChromaDB to store TravelEase FAQ documents.

ChromaDB converts text into vector embeddings and enables similarity-based retrieval.

### 3. Semantic Search

Implemented a custom `search_travel_faq` tool to retrieve relevant information from the knowledge base based on customer questions.

This allows the agent to retrieve information even when the customer's wording differs from the stored FAQ.

### 4. RAG Integration

Integrated the FAQ search tool into the existing TravelEase AI agent.

The agent retrieves relevant information before answering general questions about packages and booking policies.

### 5. Conversation Memory

Implemented conversation memory using LangGraph's `InMemorySaver`.

This allows the agent to remember previous messages within the same conversation.

### 6. Thread-Based Conversation Management

Used unique thread IDs to maintain separate conversations for different customers.

- Same thread ID: Maintains conversation context.
- Different thread ID: Maintains an independent conversation.

## Architecture

Customer Question → TravelEase AI Agent → RAG Search / Booking Tools / Conversation Memory → Context-Aware Response

## Testing and Results

| Test | Expected Behaviour | Result |
|---|---|---|
| Test 1 | Retrieve Manali package duration and price | Passed |
| Test 2 | Remember previous package information | Passed |
| Test 3 | Isolate different customer conversations | Passed |
| Test 4 | Handle unsupported Switzerland destination without inventing package details | Passed |

## Key Learnings

- Understanding the RAG architecture.
- Working with vector databases and embeddings.
- Implementing semantic search.
- Integrating retrieval tools with AI agents.
- Maintaining conversational context.
- Managing independent customer sessions using thread IDs.
- Reducing unsupported or hallucinated responses through knowledge-grounded retrieval.

## Conclusion

Successfully extended the TravelEase AI Booking Assistant with Retrieval-Augmented Generation and conversation memory.

The agent can retrieve relevant travel information from a custom knowledge base, remember previous conversations within a thread, and handle unsupported destination queries more reliably.

**Note:** The current implementation uses in-memory conversation storage. Conversation history is not persistent across runtime restarts.