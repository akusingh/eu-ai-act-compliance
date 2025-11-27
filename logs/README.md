# Logs Directory

This directory contains execution logs from the EU AI Act Compliance Agent.

## Log Files

Logs are automatically created during agent execution and include:

- **Timestamp** - When the operation occurred
- **Log Level** - INFO, WARNING, ERROR, DEBUG
- **Component** - Which module generated the log
- **Message** - Details about the operation
- **Context** - Additional structured data

## Log Naming Convention

Logs are named with timestamps for easy identification:

```
web_demo_YYYYMMDD_HHMMSS.log
evaluation_YYYYMMDD_HHMMSS.log
agent_run_YYYYMMDD_HHMMSS.log
```

## Log Format

Logs use structured JSON format for easy parsing:

```json
{
  "timestamp": "2025-11-27T10:30:45.123456",
  "level": "INFO",
  "logger": "src.sequential_orchestrator",
  "message": "Starting compliance assessment",
  "query": "facial recognition system",
  "agent_count": 5
}
```

## Usage

Logs are automatically generated when running:

```bash
# Web demo logs
python web_demo.py
# Creates: logs/web_demo_YYYYMMDD_HHMMSS.log

# Evaluation logs
python evaluate.py
# Creates: logs/evaluation_YYYYMMDD_HHMMSS.log

# Demo logs
python demo_final.py
# Creates: logs/agent_run_YYYYMMDD_HHMMSS.log
```

## Configuration

Logging configuration is managed in `src/observability.py`:

- **Console output:** INFO level and above
- **File output:** DEBUG level and above
- **Format:** Structured JSON with timestamps
- **Rotation:** Not implemented (manual cleanup needed)

## Analyzing Logs

Use standard tools to analyze logs:

```bash
# View recent logs
tail -f logs/web_demo_*.log

# Search for errors
grep "ERROR" logs/*.log

# Parse JSON logs with jq
cat logs/web_demo_*.log | jq '.message'
```

## Cleanup

Logs are not automatically deleted. To clean up old logs:

```bash
# Remove logs older than 7 days
find logs/ -name "*.log" -mtime +7 -delete

# Remove all logs
rm -f logs/*.log
```

## Note

This directory is included in `.gitignore` to prevent committing log files to the repository.
