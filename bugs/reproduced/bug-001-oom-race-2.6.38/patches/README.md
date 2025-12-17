# Bug #001 Patches

## Debug Patches (Internal Use)
Applied these to understand the bug. NOT for upstream.

1. [0001-add-oom-debug-prints.patch](debug/0001-add-oom-debug-prints.patch)
   - Adds pr_info in select_bad_process()
   - Shows victim selection timing
   - Generated: [dmesg-with-debug.txt](../logs/original/dmesg-with-debug.txt)

2. [0002-trace-victim-selection.patch](debug/0002-trace-victim-selection.patch)
   - Dumps all candidate processes
   - Shows badness scores

## Fix Patches

### v1 (Failed)
[fix/v1/0001-mm-oom-fix-race.patch](fix/v1/0001-mm-oom-fix-race.patch)

**Problem:** Still had race in corner case  
**Why:** Lock too narrow  
**Test:** Still crashed 1/10 times

### v2 (Better)
[fix/v2/0001-mm-oom-fix-race.patch](fix/v2/0001-mm-oom-fix-race.patch)

**Changes:** Widened lock scope  
**Test:** No crash in 100 iterations  
**Problem:** Performance regression (20% slower)

### v3 (Final)
[fix/v3/0001-mm-oom-fix-race.patch](fix/v3/0001-mm-oom-fix-race.patch)

**Changes:** Use RCU instead of spinlock  
**Test:** ✓ No crashes, ✓ No performance loss  
**Status:** Ready for submission

## Upstream Status
- [ ] Submitted to LKML
- [ ] Received feedback
- [ ] Revised patch
- [ ] Accepted
- [ ] Merged
```

---

### 3. Complete Bug Directory Example
```
bug-001-oom-race-2.6.38/
├── README.md                           # Bug overview
│
├── reproduction.md                     # How to trigger
│
├── root-cause.md                       # Analysis
│
├── fix.md                             # Solution explanation
│
├── logs/                              # ALL DMESG HERE
│   ├── original/
│   │   ├── dmesg-original.txt         # Bug behavior
│   │   ├── dmesg-with-debug.txt       # With debug patch
│   │   └── ftrace-original.txt
│   ├── with-fix/
│   │   ├── dmesg-fixed.txt            # After fix applied
│   │   ├── dmesg-stress-test.txt
│   │   └── comparison.md
│   └── README.md
│
├── patches/                           # ALL PATCHES HERE
│   ├── debug/
│   │   ├── 0001-add-debug-prints.patch
│   │   └── 0002-trace-selection.patch
│   ├── fix/
│   │   ├── v1/
│   │   ├── v2/
│   │   ├── v3/
│   │   └── final/
│   │       └── 0001-mm-oom-fix-race.patch
│   └── README.md
│
├── tests/                             # Test scripts
│   ├── reproduce.sh
│   ├── test-fix.sh
│   └── stress-test.sh
│
└── artifacts/                         # Other debug data
    ├── vmcore
    ├── gdb-session.txt
    └── perf.data
