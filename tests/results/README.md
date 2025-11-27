# Test Results Directory

This directory contains **actual test execution results** in JSON format.

## Files

- **`test_results_latest.json`** - Always contains the most recent test run
- **`test_results_YYYYMMDD_HHMMSS.json`** - Timestamped historical runs

## What's Inside

Each JSON file contains:
- ✅ Test outcomes (passed/failed/skipped)
- ⏱️ Execution durations
- 📊 Summary statistics  
- 🐛 Error messages and tracebacks (for failures)
- 📍 Line numbers and test locations

## Quick View

```bash
# View latest results summary
jq '.summary' test_results_latest.json

# Example output:
# {
#   "passed": 21,
#   "total": 21,
#   "collected": 21
# }
```

## How It Works

Results are **automatically generated** every time you run pytest:

```bash
pytest tests/test_models.py -v

# Output shows:
# --------------------------------- JSON report ----------------------------------
# report saved to: tests/results/test_results_latest.json
# ========================== 21 passed in 0.06s ===============================
```

## What's Different From Test Documentation?

| Feature | Test Docs (`tests/docs/`) | Test Results (`tests/results/`) |
|---------|---------------------------|----------------------------------|
| **Content** | What tests exist | What happened when they ran |
| **Type** | Static (test structure) | Dynamic (execution outcomes) |
| **Updates** | When test code changes | Every pytest run |
| **Purpose** | Documentation | Verification & monitoring |
| **Example** | "test_all_risk_tiers_defined checks that all four risk tiers are defined" | "test_all_risk_tiers_defined: PASSED in 0.0001s" |

## Typical Results File

```json
{
  "created": 1763464620.744565,
  "duration": 0.064,
  "exitcode": 0,
  "summary": {
    "passed": 21,
    "failed": 0,
    "skipped": 0,
    "total": 21
  },
  "tests": [
    {
      "nodeid": "tests/test_models.py::TestRiskTierEnum::test_all_risk_tiers_defined",
      "outcome": "passed",
      "call": {
        "duration": 0.0001,
        "outcome": "passed"
      }
    }
    // ... more tests
  ]
}
```

## Query Examples

### Get pass rate:
```bash
jq '.summary | (.passed / .total * 100)' test_results_latest.json
# Output: 100
```

### List failed tests:
```bash
jq '.tests[] | select(.outcome == "failed") | .nodeid' test_results_latest.json
```

### Find slowest test:
```bash
jq '.tests | sort_by(.call.duration) | reverse | first | {test: .nodeid, duration: .call.duration}' test_results_latest.json
```

## Complete Guide

See `TEST_RESULTS_JSON_GUIDE.md` in the project root for:
- Full JSON structure documentation
- Advanced query examples
- Python integration examples
- CI/CD usage patterns

---

**Auto-generated** by pytest-json-report plugin 📊
