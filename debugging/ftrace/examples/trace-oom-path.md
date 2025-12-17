# Example: Trace OOM Killer Path

## Goal
See complete call path when OOM killer executes.

## Method 1: Manual ftrace
```bash
cd /sys/kernel/debug/tracing

# Set function_graph tracer
echo function_graph > current_tracer

# Filter OOM functions
echo '*oom*' > set_ftrace_filter

# Clear buffer
echo > trace

# Enable
echo 1 > tracing_on

# Trigger OOM
stress-ng --vm 1 --vm-bytes 2G &

# Wait for OOM, then stop
echo 0 > tracing_on

# View trace
cat trace > ~/oom-trace.txt
```

## Method 2: trace-cmd
```bash
# Record
trace-cmd record -p function_graph -l '*oom*' &

# Trigger OOM
stress-ng --vm 1 --vm-bytes 2G

# Stop trace (Ctrl+C)

# View
trace-cmd report > oom-trace.txt
```

## Output
See: [traces/oom-trace.txt](traces/oom-trace.txt)

**Key Path:**
```
do_page_fault()
  handle_mm_fault()
    __alloc_pages()
      __alloc_pages_slowpath()
        __alloc_pages_may_oom()
          out_of_memory()
            select_bad_process()
            oom_kill_process()
```

## What I Learned
- OOM triggered from page fault path
- Multiple retry attempts before OOM
- Victim selection takes ~50ms
