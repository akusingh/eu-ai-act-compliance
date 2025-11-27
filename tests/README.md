# Tests Directory

Comprehensive test suite for the EU AI Act Compliance Agent.

## Test Structure

```
tests/
├── test_models.py              # Pydantic model validation (21 tests)
├── test_orchestrator.py        # Agent orchestration logic (18 tests)
├── test_tools.py               # Custom ADK tools (16 tests)
├── test_vector_search.py       # Hybrid search functionality (17 tests)
├── results/                    # Test execution results (JSON)
└── __pycache__/               # Python bytecode cache
```

## Test Coverage

### Total: 72 Unit Tests

| Module | Tests | Coverage |
|--------|-------|----------|
| `test_models.py` | 21 | Pydantic models, validation, serialization |
| `test_orchestrator.py` | 18 | Agent coordination, parallel execution |
| `test_tools.py` | 16 | Compliance scoring, EU AI Act reference |
| `test_vector_search.py` | 17 | Hybrid search, BM25, vector similarity |

## Running Tests

### Run All Tests
```bash
pytest tests/ -v
```

### Run Specific Test File
```bash
pytest tests/test_models.py -v
pytest tests/test_orchestrator.py -v
pytest tests/test_tools.py -v
pytest tests/test_vector_search.py -v
```

### Run with Coverage
```bash
pytest tests/ --cov=src --cov-report=html
```

### Run Specific Test
```bash
pytest tests/test_models.py::test_compliance_assessment_creation -v
```

## Test Categories

### 1. Model Tests (`test_models.py`)
Tests for Pydantic data models:
- ✅ Compliance assessment creation and validation
- ✅ Risk classification enum handling
- ✅ Requirement gap structures
- ✅ JSON serialization/deserialization
- ✅ Field validation and constraints

### 2. Orchestrator Tests (`test_orchestrator.py`)
Tests for agent coordination:
- ✅ Sequential pipeline execution
- ✅ Parallel research agent coordination
- ✅ State management between agents
- ✅ Error handling and recovery
- ✅ Timeout management

### 3. Tool Tests (`test_tools.py`)
Tests for custom ADK tools:
- ✅ Compliance scoring algorithm
- ✅ Risk tier calculation
- ✅ EU AI Act article retrieval
- ✅ Confidence score generation
- ✅ Reference validation

### 4. Vector Search Tests (`test_vector_search.py`)
Tests for hybrid search:
- ✅ BM25 keyword search
- ✅ Vector similarity search
- ✅ RRF fusion ranking
- ✅ Query expansion
- ✅ Result reranking

## Evaluation Scenarios

Beyond unit tests, we have 8 end-to-end evaluation scenarios in `evaluate.py`:

1. ✅ **Facial Recognition (Law Enforcement)** - Prohibited practice
2. ✅ **Social Scoring System** - Prohibited practice
3. ✅ **Medical Diagnosis AI** - High-risk system
4. ✅ **Recruitment Screening AI** - High-risk system
5. ⚠️ **Deepfake Generator** - Limited-risk (transparency)
6. ✅ **Chatbot (Customer Service)** - Minimal-risk
7. ✅ **Predictive Maintenance** - Minimal-risk
8. ⚠️ **Education Assessment AI** - High-risk

**Current Results:** 6/8 passing (75% accuracy)

## Test Results

Test results are saved in JSON format in `tests/results/`:
- `test_results_latest.json` - Most recent run
- `test_results_YYYYMMDD_HHMMSS.json` - Timestamped history

View results:
```bash
# Summary
jq '.summary' tests/results/test_results_latest.json

# Failed tests
jq '.tests[] | select(.outcome == "failed")' tests/results/test_results_latest.json
```

## Continuous Integration

Tests run automatically on:
- ✅ Every commit (GitHub Actions)
- ✅ Pull requests
- ✅ Pre-deployment checks

## Writing New Tests

Example test structure:

```python
import pytest
from src.models import ComplianceAssessment

def test_compliance_assessment_creation():
    """Test creating a valid compliance assessment."""
    assessment = ComplianceAssessment(
        risk_level="HIGH_RISK",
        confidence=0.95,
        reasoning="System processes personal data...",
        applicable_articles=["Article 6", "Article 9"]
    )
    assert assessment.risk_level == "HIGH_RISK"
    assert assessment.confidence == 0.95
```

## Dependencies

Tests require:
```bash
pytest>=7.4.0
pytest-cov>=4.1.0
pytest-asyncio>=0.21.0  # For async tests
```

## Known Issues

- ⚠️ Deepfake detection needs better pattern matching
- ⚠️ Education AI classification edge cases
- ⚠️ Parallel agent timeout handling under load

See `tests/results/README.md` for detailed test execution logs.
