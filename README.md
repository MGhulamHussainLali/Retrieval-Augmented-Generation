# Retrieval-Augmented-Generation
Adaptive RAG pipeline with fixed-size &amp; semantic chunking, vector search, and a LangGraph grader-router for multi-source question answering.
# Retrieval-Augmented Generation Pipeline

An end-to-end RAG system built from scratch on Databricks, featuring two chunking strategies, custom vector search, and an agentic LangGraph workflow that adaptively routes queries based on retrieval quality.

## Features

- **Fixed-Size Chunking** — Sliding window splitter with configurable chunk size and overlap
- **Semantic Chunking** — Embedding-based splitter that detects topic boundaries using cosine similarity between sentence embeddings
- **Vector Search** — Custom similarity search over Delta-stored embeddings using Azure OpenAI embeddings
- **RAG Pipeline** — LCEL-based retrieval and generation chain with a strict context-grounded system prompt
- **Agentic RAG (LangGraph)** — A stateful graph that grades retrieval quality and conditionally falls back to a secondary text-file knowledge source, with an LLM router classifying the query topic

## Tech Stack

`Python` `LangChain` `LangGraph` `Azure OpenAI` `Databricks` `Delta Lake` `PySpark`

## Architecture

```
Question → Retrieve (Vector Search) → Grade (LLM Grader)
                                          ↓            ↓
                                       Accept       Fallback (Text File)
                                          ↓            ↓
                                       Answer       Re-answer
```

## Chunking Strategy Comparison

| | Fixed-Size | Semantic |
|---|---|---|
| **Method** | Sliding window | Cosine similarity threshold |
| **Strengths** | Breadth, precise recall | Coherent, topic-aligned chunks |
| **Best for** | Exact factual lookups | Conceptual questions |
