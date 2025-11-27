# Scripts Directory

Utility scripts for data processing, index building, and project setup.

## Available Scripts

### Data Processing

#### `download_eu_ai_act.sh`
Downloads the official EU AI Act text from EUR-Lex.

```bash
./scripts/download_eu_ai_act.sh
```

**Output:** `data/eu_ai_act_full.txt`

#### `split_eu_ai_act.py`
Splits the EU AI Act into structured sections (articles, recitals, annexes).

```bash
python scripts/split_eu_ai_act.py
```

**Outputs:**
- `data/eu_act_articles.txt`
- `data/eu_act_recitals.txt`
- `data/eu_act_annexes.txt`

### Vector Index Building

#### `build_vector_indexes.py`
Builds FAISS vector indexes for semantic search across the EU AI Act.

```bash
python scripts/build_vector_indexes.py
```

**Features:**
- Chunks documents into manageable segments
- Generates embeddings using Google's Gemini API
- Creates FAISS indexes for fast similarity search
- Saves indexes to `data/embeddings_cache/`

**Configuration:**
- Chunk size: 1000 tokens
- Overlap: 200 tokens
- Embedding model: `models/embedding-001`

**Outputs:**
- `data/embeddings_cache/annexes/eu_ai_act_index.pkl`
- `data/embeddings_cache/articles/eu_ai_act_index.pkl`
- `data/embeddings_cache/recitals/eu_ai_act_index.pkl`

## Setup Requirements

All scripts require:
```bash
# Install dependencies
pip install -r requirements.txt

# Set API key
export GOOGLE_GENAI_API_KEY="your-api-key"
```

## Usage Workflow

Typical setup workflow:

```bash
# 1. Download the EU AI Act
./scripts/download_eu_ai_act.sh

# 2. Split into sections
python scripts/split_eu_ai_act.py

# 3. Build vector indexes
python scripts/build_vector_indexes.py
```

After running these scripts, the agent will have access to:
- Structured EU AI Act text
- Fast semantic search capabilities
- Pre-computed embeddings for quick startup

## Notes

- Vector index building can take 5-10 minutes depending on API rate limits
- Indexes are cached and don't need to be rebuilt unless the source text changes
- The `data/embeddings_cache/` directory should be committed to avoid rebuilding indexes
