# Research Tools

## Stress Tests
### oom-trigger.sh
Triggers system OOM killer.
```bash
./tools/stress-tests/oom-trigger.sh
```

### memcg-stress.sh
Stress test cgroup memory limit.
```bash
./tools/stress-tests/memcg-stress.sh 100M
```

## Analysis Tools
### parse-dmesg.py
Extract OOM kills from dmesg.
```bash
python3 tools/analysis/parse-dmesg.py dmesg.txt
```

### compare-logs.sh
Compare two dmesg files.
```bash
./tools/analysis/compare-logs.sh before.txt after.txt
```

## Tracing
### ftrace-setup.sh
Setup ftrace for OOM events.
```bash
./tools/tracing/ftrace-setup.sh
```

### perf-record.sh
Record performance data.
```bash
./tools/tracing/perf-record.sh stress-test
```

## Installation
```bash
# Make executable
chmod +x tools/**/*.sh

# Add to PATH (optional)
export PATH=$PATH:$(pwd)/tools/stress-tests
```
