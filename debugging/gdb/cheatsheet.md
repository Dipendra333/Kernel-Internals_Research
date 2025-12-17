# GDB Kernel Debugging Cheatsheet

## Start GDB Session
```bash
# Terminal 1: Start QEMU with GDB
qemu-system-x86_64 -kernel bzImage -s -S

# Terminal 2: Connect GDB
gdb vmlinux
(gdb) target remote :1234
```

## Breakpoints
```bash
# Set breakpoint
break oom_kill_process
break mm/oom_kill.c:500

# Conditional breakpoint
break oom_kill_process if victim->pid == 1234

# List breakpoints
info breakpoints

# Delete breakpoint
delete 1
```

## Execution
```bash
continue    # Continue execution
next       # Next line (step over)
step       # Step into function
finish     # Finish current function
```

## Inspection
```bash
# Print variable
print victim->pid
print *memcg

# Print structure
print *task
p *task->mm

# Display (auto-print)
display victim->comm

# Backtrace
bt
```

## Memory
```bash
# Examine memory
x/10x 0xffffffff81234567

# Print string
x/s task->comm
```

## Advanced
```bash
# Call function
call dump_stack()

# Set variable
set variable x = 5

# Load symbols
add-symbol-file module.ko 0xaddress
```
