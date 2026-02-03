# System Architecture

## Overview

This system implements a multi-stage AI pipeline for automated research proposal generation. The architecture follows an agentic pattern where each stage processes and enriches data before passing to the next.

## Pipeline Stages

### Stage 1: Document Ingestion
- **Input**: NOFO PDF, Research paper PDFs
- **Processing**: PyPDF extraction, text chunking (1000 tokens, 200 overlap)
- **Output**: Document objects with metadata

### Stage 2: Topic Extraction
- **Input**: NOFO document content
- **Processing**: LLM prompt to identify funding priorities
- **Output**: Structured topic description

### Stage 3: Relevance Assessment
- **Input**: Research papers, extracted topic
- **Processing**: 
  - BM25 keyword scoring
  - Semantic embedding similarity (sentence-transformers)
  - Hybrid score combination
- **Output**: Filtered list of relevant papers with summaries

### Stage 4: Vector Store Creation
- **Input**: Filtered relevant papers
- **Processing**: ChromaDB indexing with embeddings
- **Output**: Searchable vector store

### Stage 5: Proposal Ideation
- **Input**: Topic, relevant papers, NOFO requirements
- **Processing**: LLM generates 5 distinct proposals
- **Output**: Structured proposal ideas with citations

### Stage 6: RAG-Enhanced Drafting
- **Input**: Selected proposal idea, vector store
- **Processing**: Retrieve relevant chunks, generate full sections
- **Output**: Complete proposal draft

## Key Design Decisions

### Hybrid Retrieval
Combined BM25 (keyword) and semantic search to capture both exact matches and conceptual similarity. This outperforms either method alone for academic content.

### Structured Output Prompts
Used delimiter-based formatting (`---`) to ensure consistent, parseable LLM outputs for downstream processing.

### Chunking Strategy
1000-token chunks with 200-token overlap balances context preservation with retrieval precision.

## Performance Characteristics

| Stage | Latency | Token Usage |
|-------|---------|-------------|
| Topic Extraction | ~2s | ~500 tokens |
| Relevance Assessment (per paper) | ~3s | ~1000 tokens |
| Proposal Ideation | ~10s | ~2000 tokens |
| RAG Drafting | ~15s | ~3000 tokens |

## Extensibility

The modular design allows swapping components:
- Different LLMs (Claude, Llama, etc.)
- Alternative vector stores (Pinecone, Weaviate)
- Custom embedding models
- Domain-specific relevance criteria
