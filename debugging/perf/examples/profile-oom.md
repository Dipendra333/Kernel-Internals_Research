# Example: Profile OOM Killer Performance

## Goal
Find where OOM killer spends time.

## Method
```bash
# Record OOM event
perf record -e kmem:mm_page_alloc -a -g &

# Trigger OOM
stress-ng --vm 1 --vm-bytes 2G

# Stop recording (Ctrl+C)

# Generate report
perf report > oom-profile.txt

# Flamegraph (optional)
perf script | flamegraph.pl > oom-flame.svg
```

## Results
See: [data/oom-profile.txt](data/oom-profile.txt)

**Top Functions:**
```
45%  select_bad_process
30%  oom_scan_process_thread
15%  oom_badness
10%  oom_kill_process
```

## Analysis
Most time in victim selection (select_bad_process).

## Optimization Ideas
- Cache badness scores
- Parallel victim scanning
