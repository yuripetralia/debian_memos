# System Management in Linux

This guide covers essential system management tasks, monitoring, and administration in Linux systems.

## Table of Contents
- [System Information](#system-information)
- [Service Management](#service-management)
- [User Management](#user-management)
- [Resource Monitoring](#resource-monitoring)
- [Storage Management](#storage-management)
- [System Maintenance](#system-maintenance)
- [Log Management](#log-management)
- [Backup and Recovery](#backup-and-recovery)

## System Information

### Basic System Information
```bash
# Kernel information
uname -a                    # All system information
uname -r                    # Kernel release
uname -m                    # Machine hardware name

# Distribution information
lsb_release -a             # Distribution information
cat /etc/os-release        # OS information
hostnamectl                # System and OS information

# Hardware information
lshw                       # Hardware configuration
lscpu                      # CPU information
lsblk                      # Block devices
lspci                      # PCI devices
lsusb                      # USB devices
```

### System Resources
```bash
# Memory information
free -h                    # RAM usage
cat /proc/meminfo          # Detailed memory info

# CPU information
cat /proc/cpuinfo          # CPU details
uptime                     # System load average

# Disk space
df -h                      # Disk usage
du -sh [directory]         # Directory size
```

## Service Management

### Systemd Service Control
```bash
# Basic service operations
systemctl start [service]      # Start service
systemctl stop [service]       # Stop service
systemctl restart [service]    # Restart service
systemctl reload [service]     # Reload configuration
systemctl status [service]     # Check service status

# Service management
systemctl enable [service]     # Enable at boot
systemctl disable [service]    # Disable at boot
systemctl is-enabled [service] # Check if enabled
systemctl mask [service]       # Completely disable service
systemctl unmask [service]     # Remove masking

# System targets
systemctl get-default         # Show default target
systemctl set-default [target]# Set default target
systemctl isolate [target]    # Change current target
```

### Service Information
```bash
# List services
systemctl list-units --type=service             # Running services
systemctl list-units --type=service --all       # All services
systemctl list-unit-files --type=service        # Service files

# View service configuration
systemctl cat [service]                         # View service file
systemctl show [service]                        # Show properties
journalctl -u [service]                         # View service logs
```

## User Management

### User Administration
```bash
# Create and modify users
useradd [username]              # Create user
useradd -m -s /bin/bash [user] # Create with home and shell
usermod -aG [group] [user]     # Add user to group
userdel -r [username]          # Delete user and home

# Password management
passwd [username]              # Set password
chage -l [username]           # Password expiry info
chage -M [days] [username]    # Set maximum password age

# Group management
groupadd [groupname]          # Create group
groupdel [groupname]          # Delete group
groups [username]             # Show user groups
```

### User Information
```bash
# User information commands
id [username]                 # User and group IDs
who                          # Show who is logged in
w                            # Show who is logged in and what they're doing
last                         # Show last logins
lastlog                      # Show last login for all users
```

## Resource Monitoring

### Process Monitoring
```bash
# Process information
top                         # Interactive process viewer
htop                        # Enhanced process viewer
ps aux                      # Show all processes
pstree                      # Process tree

# Process management
kill [PID]                  # Kill process
killall [name]              # Kill by name
nice -n [value] [command]   # Run with priority
renice [value] -p [PID]     # Change priority
```

### System Monitoring
```bash
# System activity
vmstat [interval]           # Virtual memory stats
iostat [interval]           # IO statistics
sar                         # System activity reporter

# Network monitoring
netstat -tuln               # Active connections
ss -tuln                    # Socket statistics
iftop                       # Network traffic monitor
```

## Storage Management

### Disk Operations
```bash
# Disk partitioning
fdisk -l                    # List partitions
fdisk [device]              # Partition tool
parted [device]             # Advanced partition tool

# Filesystem operations
mkfs.[type] [device]        # Create filesystem
mount [device] [directory]  # Mount filesystem
umount [device]             # Unmount filesystem
fsck [device]               # Check filesystem
```

### Storage Monitoring
```bash
# Storage analysis
ncdu [directory]            # NCurses disk usage
iotop                       # IO monitoring
fstrim -av                  # TRIM SSD filesystems
```

## System Maintenance

### System Updates
```bash
# Update management
apt update                  # Update package list
apt upgrade                 # Upgrade packages
apt full-upgrade           # Full system upgrade
apt autoremove             # Remove unused packages
```

### System Cleanup
```bash
# Cleanup operations
journalctl --vacuum-time=7d # Clean old logs
apt clean                   # Clean package cache
find /tmp -type f -atime +10 -delete  # Clean old temp files
```

## Log Management

### System Logs
```bash
# Log viewing
journalctl                  # View system logs
journalctl -f              # Follow log messages
journalctl -u [service]    # Service logs
journalctl --since today   # Today's logs

# Traditional logs
tail -f /var/log/syslog    # Follow system log
grep -i error /var/log/syslog  # Search errors
zcat /var/log/syslog.*.gz  # View compressed logs
```

## Backup and Recovery

### System Backup
```bash
# Backup commands
rsync -av [source] [dest]   # Synchronize directories
dd if=[source] of=[dest]    # Disk/partition backup
tar -czf backup.tar.gz [directory]  # Archive directory
```

### System Recovery
```bash
# Recovery tools
fsck [device]               # Filesystem check
badblocks [device]          # Check for bad blocks
grub-install [device]       # Reinstall GRUB
update-grub                 # Update GRUB configuration
```

## Best Practices

1. **Regular Maintenance**
   - Schedule regular updates
   - Monitor system resources
   - Clean old logs and temporary files
   - Check system logs for errors

2. **Security**
   - Regular user audit
   - Monitor failed login attempts
   - Check for unusual system activity
   - Keep security patches up to date

3. **Performance**
   - Monitor resource usage
   - Check for memory leaks
   - Optimize service configurations
   - Regular disk maintenance

4. **Documentation**
   - Keep change logs
   - Document system configurations
   - Maintain backup schedules
   - Record troubleshooting steps

## Related Documentation
- [Package Management](package-management.md)
- [Network Operations](network-operations.md)
- [Security Practices](security-practices.md)

---

For more detailed information about specific commands, use the `man` command:
```bash
man systemctl
man journalctl
man top
```