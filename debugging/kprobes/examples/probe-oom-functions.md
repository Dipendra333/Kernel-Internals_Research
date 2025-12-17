# Example: Probe OOM Functions Dynamically

## Goal
Monitor OOM killer without rebuilding kernel.

## Method
```bash
# Enable kprobe on oom_kill_process
echo 'p:myprobe oom_kill_process victim=%di:x64' > \
    /sys/kernel/debug/tracing/kprobe_events

# Enable event
echo 1 > /sys/kernel/debug/tracing/events/kprobes/myprobe/enable

# Trigger OOM
stress-ng --vm 1 --vm-bytes 2G &

# View trace
cat /sys/kernel/debug/tracing/trace
```

## Output
```
stress-ng-1234 [001] 123.456: myprobe: victim=0xffff88800123456
```

## Advanced: Capture Arguments
```bash
# Probe with multiple args
echo 'p:oom_probe oom_kill_process victim=%di:x64 message=+0(%si):string' \
    > /sys/kernel/debug/tracing/kprobe_events
```
