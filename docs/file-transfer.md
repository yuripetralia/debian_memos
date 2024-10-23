# File Transfer Guide for Linux

A comprehensive guide for transferring files securely between systems using various Linux tools.

## Table of Contents
- [SCP (Secure Copy)](#scp-secure-copy)
- [RSYNC](#rsync)
- [SFTP](#sftp)
- [Other Transfer Methods](#other-transfer-methods)
- [Performance Optimization](#performance-optimization)
- [Security Best Practices](#security-best-practices)
- [Automation and Scripting](#automation-and-scripting)

## SCP (Secure Copy)

### Basic SCP Usage
```bash
# Basic copy operations
scp [file] user@remote:/path/      # Upload file
scp user@remote:/path/[file] .     # Download file
scp -r [directory] user@remote:/path/  # Copy directory
scp user@remote1:/path/file user@remote2:/path/  # Between remotes

# Common options
scp -p [file] user@remote:/path/   # Preserve modification times
scp -P [port] [file] user@remote:/path/  # Specify port
scp -i [key] [file] user@remote:/path/   # Use specific key
scp -l [speed] [file] user@remote:/path/ # Limit bandwidth (KB/s)
```

### Advanced SCP Features
```bash
# Multiple files
scp file1 file2 user@remote:/path/     # Copy multiple files
scp user@remote:/path/{file1,file2} .  # Download multiple files

# Using compression
scp -C [file] user@remote:/path/       # Enable compression

# Verbose output
scp -v [file] user@remote:/path/       # Show detailed progress
```

## RSYNC

### Basic RSYNC Usage
```bash
# Basic sync operations
rsync [source] [destination]           # Local sync
rsync [file] user@remote:/path/        # Upload to remote
rsync user@remote:/path/[file] .       # Download from remote
rsync -a [source] [destination]        # Archive mode

# Common options
rsync -v [source] [destination]        # Verbose output
rsync -z [source] [destination]        # Compress during transfer
rsync -P [source] [destination]        # Show progress
rsync --delete [source] [destination]  # Delete extraneous files
```

### Advanced RSYNC Features
```bash
# Directory synchronization
rsync -avz [source_dir/] [destination_dir/]  # Full directory sync
rsync -avz --delete [source/] [destination/] # Mirror sync

# Filters and exclusions
rsync --exclude='*.tmp' [source] [destination]  # Exclude pattern
rsync --exclude-from='exclude.txt' [source] [destination]  # Exclude file
rsync --include='*.txt' --exclude='*' [source] [destination]  # Include pattern

# Bandwidth limiting
rsync --bwlimit=1000 [source] [destination]  # Limit to 1000 KB/s
```

### RSYNC Best Practices
```bash
# Safe sync options
rsync -avzP --dry-run [source] [destination]  # Test run
rsync -avzP --backup --backup-dir=/path/backup [source] [destination]  # Backup

# Efficient transfers
rsync -avz --partial --partial-dir=/tmp/rsync [source] [destination]  # Resume
rsync -avz --compress-level=9 [source] [destination]  # Max compression
```

## SFTP

### Interactive SFTP
```bash
# Start SFTP session
sftp user@remote                    # Connect to remote
sftp -P [port] user@remote          # Connect on specific port

# Basic commands
pwd                                # Print working directory
lpwd                               # Local working directory
cd [directory]                     # Change remote directory
lcd [directory]                    # Change local directory
ls                                 # List remote files
lls                                # List local files
```

### SFTP File Operations
```bash
# File transfer
get [remote-file]                  # Download file
put [local-file]                   # Upload file
mget [files]                       # Download multiple files
mput [files]                       # Upload multiple files

# Directory operations
get -r [directory]                 # Download directory
put -r [directory]                 # Upload directory
```

## Other Transfer Methods

### NC (NetCat)
```bash
# File transfer using netcat
# On receiving end:
nc -l -p [port] > [file]

# On sending end:
nc [host] [port] < [file]

# Directory transfer
# On receiving end:
nc -l -p [port] | tar xvf -

# On sending end:
tar cvf - [directory] | nc [host] [port]
```

### DD
```bash
# Basic disk/partition copy
dd if=[input] of=[output] bs=4M status=progress

# Network transfer with compression
# On receiving end:
nc -l -p [port] | gzip -d | dd of=[output]

# On sending end:
dd if=[input] | gzip -c | nc [host] [port]
```

## Performance Optimization

### Transfer Speed Optimization
```bash
# RSYNC optimization
rsync -avz --compress-level=9 --partial --partial-dir=/tmp/rsync \
      --bwlimit=10000 [source] [destination]

# Parallel transfers
parallel --jobs 4 rsync -avz {} user@remote:/path/ ::: file1 file2 file3

# Using compression
rsync -avz --compress-level=9 [source] [destination]  # Best compression
rsync -avz --compress-level=1 [source] [destination]  # Fast compression
```

### Resource Management
```bash
# Control CPU usage
nice -n 19 rsync -av [source] [destination]

# Control I/O priority
ionice -c2 -n7 rsync -av [source] [destination]

# Bandwidth management
trickle -u 1000 -d 1000 scp [file] user@remote:/path/
```

## Security Best Practices

### Secure Transfer Configuration
```bash
# Use SSH keys
ssh-copy-id user@remote
scp -i ~/.ssh/id_rsa [file] user@remote:/path/

# Restrict transfer paths
rsync --safe-links [source] [destination]

# Enable logging
rsync -avz --log-file=/path/to/logfile [source] [destination]
```

### Encryption Options
```bash
# Force encryption
rsync -e "ssh -c aes256-gcm@openssh.com" [source] [destination]

# Use specific SSH configuration
rsync -e "ssh -F /path/to/config" [source] [destination]
```

## Automation and Scripting

### Automated Transfers
```bash
#!/bin/bash
# Example backup script

SOURCE="/path/to/source"
DEST="user@remote:/backup"
LOG="/var/log/backup.log"

rsync -avz --delete \
      --backup --backup-dir=/path/to/backup \
      --log-file="$LOG" \
      "$SOURCE" "$DEST"
```

### Monitoring and Notifications
```bash
#!/bin/bash
# Transfer with notification

transfer() {
    rsync -avz --progress "$1" "$2"
    if [ $? -eq 0 ]; then
        notify-send "Transfer Complete" "Successfully transferred files"
    else
        notify-send "Transfer Failed" "Error during file transfer"
    fi
}
```

## Related Documentation
- [SSH Configuration](ssh-advanced.md)
- [Security Practices](security-practices.md)
- [System Administration](system-management.md)

---

For more detailed information about specific commands, use the `man` command:
```bash
man scp
man rsync
man sftp
```