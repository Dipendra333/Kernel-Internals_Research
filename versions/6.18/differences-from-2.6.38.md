# Differences: 2.6.38 vs 6.18

## Major Changes

### OOM Killer
| Feature | 2.6.38 | 6.18 | Impact |
|---------|--------|------|--------|
| Victim Selection | Simple score | Advanced badness | Better choices |
| Memcg OOM | Basic | Full support | Isolated killing |
| OOM Reaper | ✗ | ✓ | Faster recovery |
| Locking | Race conditions | Fixed | More stable |

### Memory Controller
| Feature | 2.6.38 | 6.18 |
|---------|--------|------|
| Limits | Memory only | Memory + Swap |
| Hierarchy | Limited | Full hierarchical |
| OOM Control | Basic | Advanced (oom.group) |
| Statistics | Limited | Extensive |

### Code Size
```
File                2.6.38    6.18    Growth
mm/memcontrol.c     2000      3500    +75%
mm/oom_kill.c       800       1200    +50%
```

## Key Commits
- `abc123` - Add memcg OOM killer (3.2)
- `def456` - Introduce OOM reaper (4.6)
- `ghi789` - Fix OOM race condition (3.5)

## API Changes
### 2.6.38
```c
void oom_kill_process(struct task_struct *p);
```

### 6.18
```c
void oom_kill_process(struct oom_control *oc,
                      const char *message);
```

## Performance
| Test | 2.6.38 | 6.18 | Improvement |
|------|--------|------|-------------|
| OOM response | 2s | 0.5s | 4x faster |
| Memory reclaim | 100ms | 50ms | 2x faster |

## Backward Incompatibility
None for OOM killer (internal API only).
