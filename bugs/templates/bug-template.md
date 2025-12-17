# Bug #XXX: [Short Description]

## Metadata
- **ID:** #XXX
- **Subsystem:** [MM/FS/Net/etc]
- **Affected Versions:** [e.g., 2.6.38, 3.10]
- **Status:** [Investigating/Reproduced/Fixed]
- **Severity:** [Low/Medium/High/Critical]
- **Reporter:** [Your Name]
- **Date Found:** YYYY-MM-DD

## Summary
One-line description of the bug.

## Description
Detailed description of what's wrong.

## Impact
Who/what is affected? What breaks?

## Environment
- **Kernel:** 6.18
- **Architecture:** x86_64
- **Config:** [link to .config or key options]
- **Hardware:** 4GB RAM, 2 CPUs

## Reproduction Steps
```bash
# Step 1: Setup
mkdir /sys/fs/cgroup/test

# Step 2: Trigger
stress-ng --vm 1 --vm-bytes 2G

# Step 3: Observe
dmesg | tail -50
```

**Success Rate:** X/10 attempts

## Expected Behavior
What should happen.

## Actual Behavior
What actually happens.

## Logs
### Dmesg
See: [artifacts/dmesg.txt](artifacts/dmesg.txt)

**Key lines:**
```
[  123.456] BUG: kernel panic
[  123.457] Call trace:
```

### Traces
See: [artifacts/ftrace.txt](artifacts/ftrace.txt)

## Root Cause Analysis
### Affected Code
```c
// mm/oom_kill.c:123
static void select_bad_process(void) {
    // Missing lock here! ← BUG
    ...
}
```

### Why It Happens
Explanation of the root cause.

### Call Stack
```
do_page_fault()
  ├─ handle_mm_fault()
  │   └─ __do_fault()
  │       └─ oom_kill()  ← Race here
  └─ ...
```

## Fix
### Proposed Solution
```c
// Add lock
static void select_bad_process(void) {
    spin_lock(&oom_lock);
    ...
    spin_unlock(&oom_lock);
}
```

### Patch
See: [../../patches/in-progress/0001-fix-bug-xxx.patch]

### Testing
- [x] Compiled successfully
- [x] Bug no longer reproduces
- [ ] Regression testing
- [ ] Submit to mailing list

## References
- Original report: [link]
- Similar bug: [link]
- Kernel commit that introduced: [commit hash]
- Fix in later version: [commit hash]

## Timeline
- **2025-01-10:** Bug discovered
- **2025-01-11:** Reproduced reliably
- **2025-01-12:** Root cause identified
- **2025-01-13:** Fix developed
- **2025-01-14:** Testing
- **2025-01-15:** Patch submitted

## Status Updates
### 2025-01-15
- Submitted patch v1 to LKML
- Waiting for maintainer feedback

### 2025-01-14
- Completed testing
- No regressions found
