# Process Management in Linux

A comprehensive guide for managing, monitoring, and controlling processes in Linux systems.

## Table of Contents
- [Basic Process Management](#basic-process-management)
- [Process Monitoring](#process-monitoring)
- [Process Control](#process-control)
- [Job Control](#job-control)
- [Resource Management](#resource-management)
- [System Services](#system-services)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)

## Basic Process Management

### Viewing Processes
```bash
# List processes
ps                     # Show current shell processes
ps aux                 # Show all processes
ps -ef                 # Full format listing
ps --forest           # Show process hierarchy
ps -u [username]       # Show user processes

# Process tree
pstree                # Display tree of processes
pstree -p             # Show PIDs
pstree -a             # Show command line arguments
```

### Process Information
```bash
# Process details
top                   # Interactive process viewer
htop                  # Enhanced process viewer
pidof [program]       # Find PID of program
pgrep [pattern]       # Find processes by name
pwdx [PID]           # Show process working directory
```

## Process Monitoring

### Real-time Monitoring
```bash
# Interactive monitors
top                   # Basic process monitor
htop                  # Enhanced monitor
atop                  # Advanced system monitor
glances               # System monitoring tool

# Process statistics
vmstat [interval]     # Virtual memory stats
iostat [interval]     # IO statistics
mpstat [interval]     # CPU statistics
```

### Process Details
```bash
# Detailed information
ps -p [PID] -o pid,ppid,cmd,%cpu,%mem  # Specific process info
cat /proc/[PID]/status                 # Process status
cat /proc/[PID]/cmdline                # Command line
cat /proc/[PID]/environ                # Environment variables
lsof -p [PID]                         # Open files
```

## Process Control

### Sending Signals
```bash
# Kill commands
kill [PID]            # Send SIGTERM (15)
kill -9 [PID]         # Send SIGKILL (9)
kill -l               # List all signals
killall [name]        # Kill by process name
pkill [pattern]       # Kill by pattern

# Common signals
SIGHUP  (1)          # Hangup
SIGINT  (2)          # Interrupt (Ctrl+C)
SIGQUIT (3)          # Quit
SIGKILL (9)          # Force kill
SIGTERM (15)         # Terminate gracefully
SIGSTOP (19)         # Stop process
SIGCONT (18)         # Continue process
```

### Process Priority
```bash
# Nice values
nice -n [value] [command]    # Start with priority
renice [value] -p [PID]      # Change priority
renice [value] -u [user]     # Change user processes

# Priority values
# -20 to 19 (lower = higher priority)
# Only root can set negative values
```

## Job Control

### Background Jobs
```bash
# Job control
command &             # Start in background
Ctrl+Z               # Suspend to background
bg                   # Continue in background
fg                   # Bring to foreground
jobs                 # List jobs
jobs -l              # List jobs with PID

# Job references
fg %1                # Foreground job 1
bg %2                # Background job 2
kill %1              # Kill job 1
```

### Screen and tmux
```bash
# Screen
screen               # Start new session
screen -ls           # List sessions
screen -r [id]       # Reattach session
Ctrl+a d             # Detach session

# tmux
tmux                 # Start new session
tmux ls              # List sessions
tmux attach -t [id]  # Attach session
Ctrl+b d             # Detach session
```

## Resource Management

### CPU Management
```bash
# CPU affinity
taskset -p [PID]             # Show CPU affinity
taskset -pc [cpus] [PID]     # Set CPU affinity

# CPU limits
cpulimit -p [PID] -l [%]     # Limit CPU usage
```

### Memory Management
```bash
# Memory information
free -h                      # Show memory usage
smem                        # Sorted memory stats
vmstat                      # Virtual memory stats

# Memory limits
ulimit -v [size]            # Set virtual memory limit
ulimit -m [size]            # Set resident set size limit
```

## System Services

### Service Management
```bash
# Systemd services
systemctl status [service]   # Check service status
systemctl start [service]    # Start service
systemctl stop [service]     # Stop service
systemctl restart [service]  # Restart service
systemctl list-units        # List all units
```

### Automatic Startup
```bash
# Service enablement
systemctl enable [service]   # Enable at boot
systemctl disable [service]  # Disable at boot
systemctl is-enabled [service] # Check if enabled
```

## Troubleshooting

### Common Issues
```bash
# High CPU usage
top -c                      # Find CPU-intensive processes
ps aux --sort=-%cpu        # Sort by CPU usage
perf top                    # CPU performance analysis

# Memory issues
ps aux --sort=-%mem        # Sort by memory usage
free -h                    # Check memory usage
dmesg | grep -i "out of memory"  # Check OOM killer
```

### Process Debugging
```bash
# Debug tools
strace -p [PID]            # Trace system calls
ltrace -p [PID]            # Trace library calls
gdb -p [PID]               # Attach debugger
```

## Best Practices

1. **Process Management**
   - Use appropriate signals for process control
   - Avoid using SIGKILL unless necessary
   - Monitor system resources regularly
   - Document critical processes

2. **Resource Control**
   - Set appropriate process priorities
   - Use resource limits when needed
   - Monitor resource usage
   - Plan for scalability

3. **Service Management**
   - Keep services updated
   - Monitor service logs
   - Use proper startup/shutdown procedures
   - Implement service monitoring

4. **Monitoring**
   - Set up resource monitoring
   - Configure alerts for critical issues
   - Keep historical data
   - Review performance regularly

## Advanced Tools and Techniques

### Process Monitoring Tools
```bash
# Advanced monitoring
iotop                       # IO monitoring
nethogs                    # Per-process network usage
fatrace                    # File access events
sysdig                     # System activity recording
```

### Resource Control
```bash
# Cgroups
cgcreate -g cpu,memory:[group]      # Create cgroup
cgset -r cpu.shares=512 [group]     # Set CPU shares
cgexec -g cpu,memory:[group] [command]  # Execute in cgroup
```

### Process Isolation
```bash
# Namespaces and containers
unshare --fork --pid --mount-proc   # Create PID namespace
chroot [directory]                  # Change root directory
```

## Related Documentation
- [System Management](system-management.md)
- [Resource Monitoring](resource-monitoring.md)
- [System Services](system-services.md)

---

For more detailed information about specific commands, use the `man` command:
```bash
man ps
man top
man kill
```