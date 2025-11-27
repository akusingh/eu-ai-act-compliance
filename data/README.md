# Data Directory

This directory contains the EU AI Act legislation data and vector embeddings used by the compliance agent.

## Contents

### Source Documents
- `eu_act_articles.txt` - All articles from the EU AI Act
- `eu_act_recitals.txt` - All recitals (preamble) from the EU AI Act
- `eu_act_annexes.txt` - All annexes from the EU AI Act
- `eu_ai_act_full.txt` - Complete EU AI Act text
- `eu_ai_act_clean.txt` - Cleaned version for processing

### Vector Embeddings Cache
- `embeddings_cache/` - Pre-computed vector embeddings for fast semantic search
  - `eu_ai_act_index.pkl` - Pickled FAISS index for hybrid search
  - `annexes/`, `articles/`, `recitals/` - Section-specific indexes

## Purpose

The data files contain the complete text of the EU AI Act (Regulation 2024/1689) which came into effect in August 2024. The agent uses these documents to:

1. **Risk Classification** - Determine if AI systems fall under prohibited, high-risk, limited-risk, or minimal-risk categories
2. **Compliance Assessment** - Identify specific requirements and obligations
3. **Reference Retrieval** - Provide exact article citations and regulatory text
4. **Gap Analysis** - Compare user's AI system against regulatory requirements

## Vector Indexes

The embeddings cache contains pre-computed vector representations of the EU AI Act text, enabling:
- Fast semantic search (< 1 second)
- Hybrid search combining BM25 and vector similarity
- Contextual retrieval of relevant regulations

These indexes are automatically loaded on startup to avoid re-computing embeddings for each query.

## Data Source

The EU AI Act text is sourced from the official EUR-Lex publication:
- **Regulation (EU) 2024/1689** - Artificial Intelligence Act
- Published: August 1, 2024
- Effective: August 2, 2024

## Usage

The data is accessed through:
- `src/vector_index_tool.py` - Vector search functionality
- `scripts/build_vector_indexes.py` - Index building script
- `scripts/split_eu_ai_act.py` - Document preprocessing script
