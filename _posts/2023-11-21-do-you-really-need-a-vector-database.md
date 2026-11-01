---
title: Do You Really Need a Vector Database?
date: 2023-11-21 22:50 +0200
categories: [LLMs, GenAI, VectorDBs, Embeddings]
tags: [llms, genai, vectordbs, embeddings]
author: tremo
description: "Exploring alternatives to vector databases for LLM applications, including FAISS, PostgreSQL pgvector, and Elasticsearch."
---

## Start with the retrieval problem

Everywhere I go, I see his face – "VectorDBs". Seriously, with the rise of GenAI and the growing number of applications utilizing Large Language Models (LLMs), Vector Databases have been posited as a de facto component in any LLM-powered application architecture. You might wonder why. The answer is seemingly straightforward: "LLMs have a limited context window, and to select the most relevant data, a VectorDB is necessary." This seems logical at first, but let's think more about it and consider the alternatives.

![Desktop View](/assets/img/posts/2023-11-21-vector-database/VectorDBs-meme.jpg){: width="500"}
_Spiderman meme of seeing vector databases everywhere_

### 1. Why Vector Search over Keyword Search?

Vector search is useful when relevant results use different words from the query. Keyword search is a strong starting point for exact terms, identifiers, and rare names. Neither is always more accurate or faster: that depends on your queries, data, index, and latency budget.

Keyword search excels in finding exact matches and can be easily updated with synonyms and taxonomies. In contrast, Vector search requires a vectorizer (embedding model) to process every query, which can incur additional costs and latency. It's also susceptible to data drift, as the embedding model might become outdated, missing new terminology and relationships.

Before adding a vector database, compare keyword, vector, and hybrid retrieval on representative queries. Measure relevance, latency, update costs, and operational complexity. A simpler system may already meet your needs.

### 2. Why Vector Database over a Vector Index?

If you still think Vector Search is more suitable for your case, consider using a Vector Index like Facebook's "FAISS," which supports the most popular indexing algorithms like "HNSW" and various similarity measures such as "L2 distance", "dot products", and cosine similarity. It can also handle indices that don’t fit in-memory.

### 3. Why Vector Database over a General-Purpose Database?

PostgreSQL with pgvector lets you keep vectors alongside relational data, with PostgreSQL's transactions, joins, and backup tooling. Elasticsearch also supports vector search alongside keyword search. Their capabilities and trade-offs differ, so start by checking what your existing database or search engine can do before introducing another service.

### When a dedicated vector database makes sense
Vector Databases definitely have their specialized use cases, especially for users managing billions of data embeddings. They benefit from architecture decisions that can improve performance over general-purpose databases, ensuring efficient storage of vectors and fast retrieval for similarity search calculations, while offering data safety. However, they aren’t the universal solution they're often portrayed as.

**Further Readings:**

- [Beware Tunnel Vision in AI Retrieval - by Colin Harman](https://colinharman.substack.com/p/beware-tunnel-vision-in-ai-retrieval)
- [Do you actually need a vector database? - Ethan Rosenthal](https://www.ethanrosenthal.com/2023/04/10/nn-vs-ann/)

---

**Related:** For more on LLM infrastructure, check out my posts on [How to Efficiently Serve an LLM?](/posts/How-to-Efficiently-serve-an-llm/) and [What Infrastructure does it take to train a 405B model?](/posts/What-Infra-does-it-take-to-train-llama405b/)
