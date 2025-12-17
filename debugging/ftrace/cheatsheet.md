# ftrace Cheatsheet

## Enable ftrace
```bash
# Check if available
cat /sys/kernel/debug/tracing/available_tracers

# Enable function tracer
echo function > /sys/kernel/debug/tracing/current_tracer

# Start tracing
echo 1 > /sys/kernel/debug/tracing/tracing_on
```

## Common Tracers
```bash
function          # Trace all functions
function_graph    # Call graph
nop              # Disable
```

## Filter Functions
```bash
# Trace only OOM functions
echo '*oom*' > /sys/kernel/debug/tracing/set_ftrace_filter

# Exclude functions
echo '!schedule' > /sys/kernel/debug/tracing/set_ftrace_notrace
```

## View Trace
```bash
cat /sys/kernel/debug/tracing/trace
```

## Clear Trace
```bash
echo > /sys/kernel/debug/tracing/trace
```

## trace-cmd (easier)
```bash
# Record
trace-cmd record -p function -l '*oom*'

# Report
trace-cmd report
```
