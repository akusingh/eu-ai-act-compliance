# Source Code (`src/`)

Core implementation of the EU AI Act Compliance Agent using Google's Agentic Development Kit (ADK).

## Architecture

The agent follows a **multi-agent orchestration pattern** with specialized research agents coordinated by an aggregator.

## Core Modules

### Agent Orchestration
- **`sequential_orchestrator.py`** - Main orchestrator coordinating multiple specialized agents
  - Manages workflow between research and aggregation phases
  - Handles parallel execution of research agents
  - Coordinates final compliance assessment

- **`parallel_research_agents.py`** - Specialized research agents for different EU AI Act aspects:
  - Risk Classification Agent
  - Prohibited Practices Agent
  - High-Risk Requirements Agent
  - Transparency Obligations Agent
  - Market Surveillance Agent

- **`aggregator_agents.py`** - Synthesis and final assessment agents:
  - Aggregates findings from all research agents
  - Produces comprehensive compliance reports
  - Generates actionable recommendations

### Tools & Utilities
- **`tools_adk.py`** - Custom ADK tools for compliance assessment:
  - `ComplianceScoringTool` - Calculates compliance scores
  - `EUAIActReferenceTool` - Retrieves specific EU AI Act articles

- **`vector_index_tool.py`** - Hybrid search implementation:
  - Combines BM25 keyword search with vector similarity
  - FAISS-based semantic search
  - Cross-encoder reranking (optional)

- **`reranker_tool.py`** - Advanced reranking for search results:
  - Cross-source result merging
  - Relevance-based reordering
  - Cohere reranker integration (optional)

### Data Models & Configuration
- **`models.py`** - Pydantic data models:
  - `ComplianceAssessment` - Structured compliance reports
  - `RiskClassification` - Risk level determinations
  - `RequirementGap` - Compliance gap analysis

- **`config.py`** - Configuration management:
  - API key handling
  - Model selection (Gemini models)
  - Environment variable loading

### Observability
- **`observability.py`** - Logging and monitoring:
  - Structured logging with `structlog`
  - Execution tracing
  - Performance metrics

- **`evaluation.py`** - Agent evaluation framework:
  - Benchmarking against test scenarios
  - Accuracy and performance metrics
  - JSON-based test case execution

## Agent Workflow

```
User Query → Sequential Orchestrator
              ↓
         Parallel Research Phase
         ├── Risk Classification Agent
         ├── Prohibited Practices Agent  
         ├── High-Risk Requirements Agent
         ├── Transparency Agent
         └── Market Surveillance Agent
              ↓
         Aggregation Phase
         └── Aggregator Agent
              ↓
         Final Compliance Report
```

## Key Technologies

- **Google ADK** - Agent framework and orchestration
- **Gemini 2.0 Flash** - LLM for agent reasoning
- **FAISS** - Vector similarity search
- **BM25** - Keyword-based retrieval
- **Pydantic** - Data validation and serialization
- **structlog** - Structured logging

## Usage

```python
from src.sequential_orchestrator import SequentialOrchestrator
from src.config import Config

# Initialize orchestrator
orchestrator = SequentialOrchestrator(Config.GOOGLE_GENAI_API_KEY)

# Run compliance assessment
result = await orchestrator.run_compliance_assessment(
    "We are building a facial recognition system for law enforcement"
)
```

## Testing

Tests are located in the `../tests/` directory. See `../tests/README.md` for details.
