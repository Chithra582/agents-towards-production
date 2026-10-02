---
name: "agent-memory-persistence"
description: "Implements durable working, episodic, and semantic memory tiers using vector indices and key-value stores."
license: MIT
---

# Agent Memory Persistence

## Overview
This skill operationalizes enterprise-grade memory architectures for conversational agents, combining low-latency key-value stores with vector embeddings and knowledge graphs.

## Key Capabilities
- **Multi-Tier Memory Architecture**: Separates fast session buffers (Redis) from long-term episodic retrieval (Mem0, Cognee).
- **Context Optimization**: Compresses historical conversation turns and filters redundant context to protect token budgets.
- **Tenant Isolation**: Partitions memory stores with cryptographic namespace keys to enforce tenant privacy.

## Operational Workflow
1. **Memory Tier Selection**: Match persistence requirements to appropriate storage engines (Redis, Qdrant, Mem0).
2. **Schema Configuration**: Establish user, session, and agent memory namespaces.
3. **Retrieval Pipeline**: Implement hybrid dense/sparse search with recency weighting and relevance reranking.
4. **Lifecycle Management**: Configure automated TTL expiration and episodic summarization jobs.
