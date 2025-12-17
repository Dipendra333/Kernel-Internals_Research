# Linux Kernel Research

My journey learning Linux kernel internals and contributing upstream.

## 👤 About
**Focus:** Memory Management, Cgroups, OOM Killer  
**Current Kernel:** 6.18  
**Started:** December 2025

## 🎯 Goals
- [ ] Understand memory management subsystem
- [ ] Reproduce and fix  bugs
- [ ] Submit 5 patches upstream
- [ ] Deep dive into 5 subsystems

## 📚 Subsystems Explored
| Subsystem | Progress | Status |
|-----------|----------|--------|
| Memory Management | 60% | 🟢 Active |
| Cgroups | 40% | 🟢 Active |
| Process Management | 10% | 🟡 Learning |
| Filesystem (VFS) | 5% | 🟡 Learning |
| Networking | 0% | ⚪ Planned |

## 🐛 Bugs Tracked
| Bug | Status | Subsystem | Version |
|-----|--------|-----------|---------|
| [#001 OOM Race](bugs/reproduced/bug-001-oom-race-2.6.38/) | ✅ Fixed | MM | 2.6.38 |
| [#002 Memcg Leak](bugs/reproduced/bug-002-memcg-leak/) | 🔍 Investigating | MM | 6.18 |
| [#003 Slab Corrupt](bugs/investigating/bug-003-slab-corruption/) | 🔄 Reproducing | MM | 6.18 |

## 📝 Recent Activity
**2025-01-15:** Analyzed OOM killer in 6.18  
**2025-01-14:** Traced cgroup creation at boot  
**2025-01-13:** Reproduced 2.6.38 OOM bug  

[Full Log](notes/learning-log.md)

## 🧪 Experiments
- **Total:** 2
- **This Month:** 2
- **Latest:** [Memcg OOM Trigger](experiments/2025-01/exp-003-memcg-stress/)

## 🔧 Patches
- **Submitted:** 10
- **Accepted:** updating
- **In Review:** updating
- **In Progress:** updating

[Patch Status](patches/README.md)

## 🚀 Quick Links
- [Setup Guide](setup/README.md)
- [Memory Management](subsystems/memory_management/README.md)
- [Cgroups](subsystems/memory_management/cgroups/README.md)
- [OOM Killer](subsystems/memory_management/oom_killer/README.md)
- [Bug Index](bugs/README.md)
- [Tools](tools/README.md)

## 📊 Stats
```
Kernels Analyzed:     4 (2.6.38, 3.10, 4.19, 6.18)
Subsystems:           5
Code Files Read:      156
Lines of Code:        ~15,000
Experiments:          
Dmesg Logs:           
Bugs Reproduced:      
Patches Submitted:    
```

## 📖 Learning Path
1. ✅ Memory Management Basics
2. ✅ OOM Killer (2.6.38 → 6.18)
3. ✅ Cgroups & Memory Controller
4. 🔄 Page Reclaim & LRU
5. ⏳ Slab Allocator
6. ⏳ Process Scheduler

## 🤝 Contributing
This is my personal research repo, but feedback welcome!

**Last Updated:** 2025-10-17
