# Learning Log

## 2025-01-15

### Topic: Memcg OOM Killer
**Time:** 3 hours

**What I Learned:**
- Memcg OOM only kills within cgroup
- Uses same victim selection as system OOM
- Difference: constraint parameter

**Code Analyzed:**
```c
// mm/memcontrol.c:mem_cgroup_out_of_memory()
bool mem_cgroup_out_of_memory(struct mem_cgroup *memcg, ...)
{
    // Limits killing to memcg hierarchy
    ...
}
```

**Questions:**
- Why does oom.group exist? → Answer: Kill all tasks atomically
- When is OOM reaper called? → After victim marked

**Experiments:**
- [exp-003](../experiments/2025-01/exp-003-memcg-stress/)

**Resources:**
- LWN article: https://lwn.net/...
- Commit: abc123def

**Next:**
- [ ] Test oom.group behavior
- [ ] Compare with system OOM timing

---

## 2025-01-14

### Topic: Cgroup Boot Initialization

**What I Learned:**
Only root cgroup exists at boot, systemd creates hierarchy.

**Key Functions:**
- `cgroup_init_early()` - T+0
- `cgroup_init()` - T+0.05s

**Dmesg:**
[experiments/2025-01/exp-001-cgroup-boot/logs/dmesg.txt]

**Discovery:**
3849 cgroups created in 14 seconds!

---

## 2025-01-13

### Topic: 2.6.38 OOM Bug Reproduction

**Status:** ✅ Successfully reproduced

**Bug:** Race condition causes wrong victim selection

**Root Cause:**
Missing lock in `select_bad_process()`

**Next Steps:**
- [ ] Write patch
- [ ] Test fix
- [ ] Submit upstream

---
