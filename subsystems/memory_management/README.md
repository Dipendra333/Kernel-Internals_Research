# Memory Management Subsystem

## Overview
Linux kernel memory management: allocation, reclaim, cgroups, OOM.

## Topics Covered
- [x] Page Allocator
- [x] OOM Killer
- [x] Cgroups
- [ ] Slab Allocator
- [ ] Page Reclaim
- [ ] Swap Management

## Quick Links
- [OOM Killer](oom-killer/README.md)
- [Cgroups](cgroups/README.md)
- [Page Allocator](concepts/page-allocator.md)

## Key Files (6.18)
```
mm/
├── memcontrol.c       # Memory controller (3500 lines)
├── oom_kill.c         # OOM killer (1200 lines)
├── page_alloc.c       # Page allocator (9000 lines)
└── vmscan.c           # Page reclaim (4500 lines)
```

## Experiments
- [exp1: Trigger System OOM](oom-killer/experiments/exp1-trigger-system-oom.md)
- [exp2: Memcg Limit Test](cgroups/experiments/exp2-process-migration.md)

## Version Comparison
| Feature | 2.6.38 | 6.18 | Notes |
|---------|--------|------|-------|
| OOM Killer | Basic | Advanced | Better victim selection |
| Memcg | Limited | Full | Memory + swap limits |
| Page Reclaim | Simple LRU | Multi-gen LRU | Improved in 6.0+ |

## Resources
- [Kernel docs](https://www.kernel.org/doc/html/latest/admin-guide/mm/)
- [LWN articles](../references/lwn-articles.md#memory-management)
