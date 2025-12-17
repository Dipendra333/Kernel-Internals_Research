# Bug #001 Logs

## Original (Buggy Behavior)
- [dmesg-original.txt](original/dmesg-original.txt) - First reproduction (2025-01-10)
- [dmesg-with-debug.txt](original/dmesg-with-debug.txt) - Added printk for analysis
- [ftrace-original.txt](original/ftrace-original.txt) - Function trace showing race

## With Fix
- [dmesg-fixed.txt](with-fix/dmesg-fixed.txt) - Bug no longer reproduces
- [dmesg-stress-test.txt](with-fix/dmesg-stress-test.txt) - 100 iterations, no crash
- [comparison.md](with-fix/comparison.md) - Before/after analysis

## Test Scenarios
- Light load: 1 stress process
- Heavy load: 10 stress processes
- Edge case: Low memory + high load
```

---

### 2. Patches Organization
```
patches/
├── debug/                              # Debug patches (NOT for upstream)
│   ├── 0001-add-oom-debug-prints.patch
│   ├── 0002-trace-victim-selection.patch
│   ├── 0003-dump-task-info.patch
│   └── README.md
│
├── fix/                                # Your actual fix
│   ├── v1/
│   │   ├── 0001-mm-oom-fix-race.patch
│   │   ├── notes.md                    # What's wrong with v1
│   │   └── review.md                   # Why it didn't work
│   ├── v2/
│   │   ├── 0001-mm-oom-fix-race.patch
│   │   ├── changes-from-v1.md          # What changed
│   │   └── test-results.txt
│   ├── v3/
│   │   └── 0001-mm-oom-fix-race.patch
│   └── final/
│       └── 0001-mm-oom-fix-race.patch  # Ready for upstream
│
├── upstream/                           # If submitted/accepted
│   ├── submitted-v1.patch              # What you sent
│   ├── submitted-v2.patch              # After feedback
│   ├── accepted.patch                  # Final merged
│   ├── submission-email.txt            # Your email
│   └── discussion-thread.txt           # Maintainer feedback
│
└── README.md                           # Index of all patches
