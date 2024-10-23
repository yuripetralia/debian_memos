# Linux Debian Commands - Notebooks

## Package Management
### APT (Advanced Package Tool)
- `apt update` - Update package list
- `apt upgrade` - Upgrade all installed packages
- `apt install [package]` - Install a new package
- `apt remove [package]` - Remove a package
- `apt autoremove` - Remove unnecessary packages
- `apt search [term]` - Search for a package
- `apt show [package]` - Show package information

## File and Directory Management
### Navigation
- `ls` - List directory contents
- `ls -la` - Detailed list including hidden files
- `cd [directory]` - Change directory
- `pwd` - Print working directory

### File Operations
- `cp [source] [destination]` - Copy files
- `mv [source] [destination]` - Move/rename files
- `rm [file]` - Delete file
- `rm -r [directory]` - Delete directory and contents
- `mkdir [name]` - Create directory
- `touch [name]` - Create empty file
- `chmod [permissions] [file]` - Change file permissions
- `chown [user]:[group] [file]` - Change file ownership

## System Management
### System Information
- `uname -a` - Kernel information
- `free -h` - RAM status
- `df -h` - Disk space
- `top` - Active processes (interactive)
- `htop` - Enhanced version of top (if installed)
- `cat /proc/cpuinfo` - CPU information
- `lsb_release -a` - Distribution information

### Service Management
- `systemctl start [service]` - Start service
- `systemctl stop [service]` - Stop service
- `systemctl status [service]` - Service status
- `systemctl enable [service]` - Enable auto-start
- `systemctl disable [service]` - Disable auto-start
- `systemctl restart [service]` - Restart service

### User Management
- `sudo [command]` - Execute command as administrator
- `su [user]` - Switch user
- `passwd` - Change password
- `adduser [name]` - Create new user
- `usermod` - Modify user
- `groups` - Show user groups
- `who` - Show who is logged in

## Network
### Connectivity
- `ip a` - Show network interfaces
- `ping [host]` - Connection test
- `netstat -tuln` - Show open ports
- `ss -tuln` - Modern alternative to netstat
- `curl [url]` - Transfer data from/to a server
- `wget [url]` - Download files

### SSH
- `ssh [user]@[host]` - SSH connection
- `scp [file] [user]@[host]:[path]` - Copy files via SSH
- `ssh-keygen` - Generate SSH key pair
- `ssh-copy-id [user]@[host]` - Copy SSH key to server

## Process Management
- `ps aux` - List all running processes
- `kill [pid]` - Kill process by ID
- `killall [name]` - Kill process by name
- `bg` - Send process to background
- `fg` - Bring process to foreground
- `nohup [command]` - Run command immune to hangups

## Text Processing
- `cat [file]` - Display file contents
- `less [file]` - View file contents with pagination
- `grep [pattern] [file]` - Search for pattern in file
- `head [file]` - Show first lines of file
- `tail [file]` - Show last lines of file
- `tail -f [file]` - Follow file changes in real-time

## Compression
- `tar -czf [archive.tar.gz] [directory]` - Create compressed archive
- `tar -xzf [archive.tar.gz]` - Extract compressed archive
- `zip -r [archive.zip] [directory]` - Create ZIP archive
- `unzip [archive.zip]` - Extract ZIP archive
