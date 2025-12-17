# Debugging Kernel Panics

## Step 1: Capture Crash Dump
```bash
# Setup kdump (one-time)
sudo apt install kdump-tools
sudo vi /etc/default/grub
# Add: crashkernel=512M
sudo update-grub
reboot

# After panic, vmcore in /var/crash/
```

## Step 2: Analyze with crash
```bash
crash /usr/lib/debug/boot/vmlinux-6.18 /var/crash/vmcore

crash> bt              # Backtrace
crash> log             # Kernel log
crash> ps              # Process list
crash> vm              # Memory info
```

## Step 3: Find Root Cause
```bash
# Look at panic message
crash> log | grep -i panic

# Check call stack
crash> bt -a

# Examine faulting instruction
crash> dis -l <address>
```

## Example
See: [../crash-dump/examples/analyze-panic.md]

## Common Causes
- NULL pointer dereference
- Stack overflow
- Deadlock
- Memory corruption
