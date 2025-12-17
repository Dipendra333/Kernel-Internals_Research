# Experiment #XXX: [Title]

**Date:** 2025-01-15  
**Subsystem:** Memory Management  
**Kernel:** 6.18  

## Goal
What are you trying to learn/test?

## Hypothesis
What do you expect to happen?

## Setup
### Environment
- Kernel: 6.18
- Memory: 4GB
- CPUs: 2

### Modifications
```c
// Added to mm/oom_kill.c
pr_info("LKF: Selecting victim\n");
```

### Build
```bash
make -j8
make modules_install
make install
reboot
```

## Procedure
### Step 1: Prepare
```bash
# Create cgroup
mkdir /sys/fs/cgroup/test
echo 100M > /sys/fs/cgroup/test/memory.max
```

### Step 2: Execute
```bash
# Run stress test
stress-ng --vm 1 --vm-bytes 200M &
echo $! > /sys/fs/cgroup/test/cgroup.procs
```

### Step 3: Observe
```bash
# Capture logs
dmesg -w > logs/dmesg.txt

# Monitor
watch cat /sys/fs/cgroup/test/memory.current
```

## Results
### Observation
What happened during the test?

### Dmesg Output
See: [logs/dmesg.txt](logs/dmesg.txt)

**Key findings:**
```
[  45.123] Memory cgroup out of memory: Killed process 1234
[  45.124] oom_reaper: reaped process 1234
```

### Metrics
| Metric | Value |
|--------|-------|
| Time to OOM | 2.5s |
| Victim PID | 1234 |
| Memory used | 100MB |

## Analysis
### What Worked
- OOM triggered as expected
- Correct victim selected

### What Didn't
- Delay of 500ms unexpected

### Why?
Root cause analysis...

## Conclusion
Summary of what you learned.

## Follow-up
- [ ] Test with different memory limit
- [ ] Try with multiple processes
- [ ] Compare with system OOM

## Files
- [setup.sh](setup.sh) - Setup script
- [test.sh](test.sh) - Test script
- [logs/dmesg.txt](logs/dmesg.txt) - Full dmesg
- [logs/trace.txt](logs/trace.txt) - Ftrace output
