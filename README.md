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

## Screen Command Guide
### Basic Screen Usage
- `screen` - Start a new screen session
- `screen -S [name]` - Start a new named screen session
- `screen -ls` - List all screen sessions
- `screen -r [name/ID]` - Reattach to a screen session
- `screen -d [name/ID]` - Detach a screen session
- `screen -dR [name]` - Detach and reattach to a session
- `screen -x [name/ID]` - Attach to a session that's already attached elsewhere

### Inside Screen Commands (after pressing Ctrl+a)
- `Ctrl+a d` - Detach from current session
- `Ctrl+a c` - Create new window
- `Ctrl+a n` - Switch to next window
- `Ctrl+a p` - Switch to previous window
- `Ctrl+a [0-9]` - Switch to window number 0-9
- `Ctrl+a "` - List all windows
- `Ctrl+a A` - Rename current window
- `Ctrl+a S` - Split screen horizontally
- `Ctrl+a |` - Split screen vertically
- `Ctrl+a tab` - Switch between split regions
- `Ctrl+a X` - Close current split region
- `Ctrl+a Q` - Close all split regions except current
- `Ctrl+a k` - Kill current window
- `Ctrl+a \` - Kill all windows and terminate screen
- `Ctrl+a ?` - Show help screen
- `Ctrl+a [` - Enter copy mode (use Enter to start/end selection)
- `Ctrl+a ]` - Paste copied text

### Common Screen Scenarios

#### Creating a Named Session
```bash
# Create a new named session
screen -S mysession

# Later, reattach to this session
screen -r mysession
```

#### Managing Multiple Windows
```bash
# Start screen
screen -S development

# Inside screen:
# Ctrl+a c     (create new window)
# Ctrl+a A     (name the window "server")
# Ctrl+a c     (create another window)
# Ctrl+a A     (name the window "logs")
```

#### Split Screen Workflow
```bash
# Inside screen:
# Ctrl+a S     (split horizontally)
# Ctrl+a |     (split vertically)
# Ctrl+a tab   (switch between regions)
# Ctrl+a c     (create new window in region)
```

### Screen Configuration
Create or edit `~/.screenrc` file to customize screen:
```bash
# Sample .screenrc configuration
# Show status bar
hardstatus alwayslastline
hardstatus string '%{= kG}[ %{G}%H %{g}][%= %{= kw}%?%-Lw%?%{r}(%{W}%n*%f%t%?(%u)%?%{r})%{w}%?%+Lw%?%?%= %{g}][%{B} %m-%d %{W}%c %{g}]'

# Set large scrollback buffer
defscrollback 10000

# Don't display welcome message
startup_message off

# Enable mouse scrolling
termcapinfo xterm* ti@:te@

# Start with specific windows
screen -t shell1 0
screen -t shell2 1
screen -t server 2
```

### Advanced Screen Features
- `screen -x` - Multi-user screen session
- `screen -L` - Turn on logging
- `screen -D -RR` - Reattach to a session, detaching it elsewhere if needed
- `screen -S session -X stuff "command^M"` - Send command to a screen session

### Best Practices
1. Always name your screen sessions descriptively
   ```bash
   screen -S project-backend
   screen -S logs-monitoring
   ```

2. Use window names for better organization
   ```bash
   # Inside screen, press Ctrl+a A to name windows
   # Example names: server, logs, shell, debug
   ```

3. Use logging when needed
   ```bash
   screen -L -S session-name
   # Logs will be saved to screenlog.0
   ```


4. Check for detached sessions before creating new ones
   ```bash
   screen -ls
   ```

## File Transfer with SCP and Rsync

### SCP (Secure Copy)
#### Basic Syntax
- `scp [options] [source] [destination]`

#### Common Options
- `-r` - Recursively copy directories
- `-p` - Preserve modification times and permissions
- `-P [port]` - Specify different SSH port
- `-i [identity_file]` - Specify SSH private key
- `-l [limit]` - Limit bandwidth in Kbit/s
- `-q` - Quiet mode (suppress progress)
- `-v` - Verbose mode for debugging

#### Common Usage Examples
```bash
# Copy local file to remote server
scp file.txt user@remote:/path/to/destination/

# Copy remote file to local system
scp user@remote:/path/to/file.txt /local/path/

# Copy entire directory
scp -r /local/directory user@remote:/path/to/destination/

# Copy using specific SSH port
scp -P 2222 file.txt user@remote:/path/

# Copy using specific SSH key
scp -i ~/.ssh/private_key file.txt user@remote:/path/

# Copy between two remote hosts
scp user1@remote1:/file.txt user2@remote2:/path/

# Copy preserving file attributes
scp -p file.txt user@remote:/path/
```

### Rsync (Remote Sync)
#### Basic Syntax
- `rsync [options] [source] [destination]`

#### Common Options
- `-a` - Archive mode (recursive, preserves permissions, etc.)
- `-v` - Verbose output
- `-z` - Compress during transfer
- `-P` - Show progress and allow resuming
- `--delete` - Delete files in destination that don't exist in source
- `--exclude=[pattern]` - Exclude files matching pattern
- `--include=[pattern]` - Include files matching pattern
- `--dry-run` - Simulate the transfer without making changes

#### Important Rsync Flags Explained
```bash
-a  # Archive mode, equals -rlptgoD
    # -r: recursive
    # -l: copy symlinks as symlinks
    # -p: preserve permissions
    # -t: preserve times
    # -g: preserve group
    # -o: preserve owner
    # -D: preserve device files and special files

-z  # Compress during transfer
-P  # Combine --progress and --partial
    # Shows progress and allows resuming interrupted transfers
```

#### Common Usage Examples
```bash
# Sync local directory to remote server
rsync -avzP /local/directory/ user@remote:/path/to/destination/

# Sync remote directory to local system
rsync -avzP user@remote:/path/to/directory/ /local/path/

# Sync with deletion (mirror)
rsync -avzP --delete /source/ /destination/

# Exclude specific files or directories
rsync -avzP --exclude='*.txt' --exclude='temp/' /source/ /destination/

# Dry run to see what would be transferred
rsync -avzP --dry-run /source/ /destination/

# Using specific SSH port
rsync -avzP -e 'ssh -p 2222' /source/ user@remote:/destination/

# Sync only specific file types
rsync -avzP --include='*.php' --include='*.html' --exclude='*' /source/ /destination/

# Resume interrupted transfer
rsync -avzP --partial /source/ /destination/
```

#### Best Practices
1. Always use `-avzP` for general transfers
   ```bash
   rsync -avzP /source/ /destination/
   ```

2. Test with --dry-run before large transfers
   ```bash
   rsync -avzP --dry-run /source/ /destination/
   ```

3. Use trailing slashes correctly
   ```bash
   # With trailing slash: copy contents of dir1 into dir2
   rsync -avzP /path/to/dir1/ /path/to/dir2/
   
   # Without trailing slash: copy dir1 itself into dir2
   rsync -avzP /path/to/dir1 /path/to/dir2/
   ```

4. Use `--delete` carefully
   ```bash
   # First do a dry run
   rsync -avzP --delete --dry-run /source/ /destination/
   
   # Then perform the actual sync
   rsync -avzP --delete /source/ /destination/
   ```

#### Common Rsync Scenarios
```bash
# Backup with timestamp
rsync -avzP /source/ /backup/$(date +%Y%m%d)/

# Sync while excluding version control directories
rsync -avzP --exclude='.git/' --exclude='.svn/' /source/ /destination/

# Sync only newer files
rsync -avzP --update /source/ /destination/

# Sync with bandwidth limit
rsync -avzP --bwlimit=1000 /source/ /destination/  # Limit to 1000 KB/s
```
