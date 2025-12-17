# Kernel Debugging Guide

## Overview
Collection of debugging techniques and tools learned during kernel research.

## Tools

| Tool | Use Case | Difficulty | When to Use |
|------|----------|------------|-------------|
| [printk](printk/) | Basic logging | ⭐ | Always start here |
| [ftrace](ftrace/) | Function tracing | ⭐⭐ | Trace call paths |
| [perf](perf/) | Performance profiling | ⭐⭐ | Find bottlenecks |
| [GDB](gdb/) | Interactive debugging | ⭐⭐⭐ | Step through code |
| [kprobes](kprobes/) | Dynamic tracing | ⭐⭐⭐ | Probe live kernel |
| [eBPF](ebpf/) | Advanced tracing | ⭐⭐⭐⭐ | Production tracing |
| [crash](crash-dump/) | Post-mortem analysis | ⭐⭐⭐ | After panic/crash |
| [JTAG](jtag/) | Hardware debugging | ⭐⭐⭐⭐⭐ | Early boot/embedded |

## Quick Start by Problem

### "Kernel Panicked!"
1. [Analyze crash dump](crash-dump/examples/analyze-panic.md)
2. [GDB on vmcore](gdb/examples/debug-panic.md)

### "System Hangs!"
1. [Use SysRq](techniques/debugging-hangs.md#sysrq)
2. [Capture stack traces](ftrace/examples/hang-trace.md)
3. [Check for deadlocks](techniques/debugging-locks.md)

### "OOM Killer Triggered!"
1. [Analyze dmesg](crash-dump/examples/analyze-oom-crash.md)
2. [Trace OOM path](ftrace/examples/trace-oom-path.md)
3. [Profile memory usage](perf/examples/profile-oom.md)

### "Function Not Working!"
1. [Add printk](printk/examples/add-debug-prints.md)
2. [Trace with ftrace](ftrace/examples/trace-syscall.md)
3. [Set GDB breakpoint](gdb/examples/breakpoint-examples.md)

## Cheatsheets
- [ftrace Quick Ref](ftrace/cheatsheet.md)
- [GDB Quick Ref](gdb/cheatsheet.md)
- [perf Quick Ref](perf/cheatsheet.md)
- [crash Quick Ref](crash-dump/cheatsheet.md)

## Learning Path
1. ✅ Start: printk debugging
2. ✅ Basic: ftrace function tracing
3. 🔄 Intermediate: GDB + QEMU
4. ⏳ Advanced: kprobes
5. ⏳ Expert: eBPF

## Real Examples
- [Debug OOM Killer](../subsystems/memory-management/oom-killer/debugging.md)
- [Debug Cgroup Creation](../subsystems/memory-management/cgroups/debugging.md)
- [Debug Slab Corruption](../bugs/reproduced/bug-008-slab-corruption/debugging.md)
