# Screen Command Guide for Linux

A comprehensive guide for using the GNU Screen terminal multiplexer in Linux systems.

## Table of Contents
- [Basic Usage](#basic-usage)
- [Window Management](#window-management)
- [Screen Navigation](#screen-navigation)
- [Split Screen](#split-screen)
- [Copy and Paste](#copy-and-paste)
- [Screen Configuration](#screen-configuration)
- [Advanced Features](#advanced-features)
- [Best Practices](#best-practices)

## Basic Usage

### Starting Screen
```bash
# Basic screen commands
screen                      # Start new screen session
screen -S [name]           # Start named session
screen -ls                 # List sessions
screen -r [name/ID]        # Reattach to session
screen -d [name/ID]        # Detach session
screen -dR [name]          # Detach and reattach
screen -x [name/ID]        # Attach to attached session
```

### Session Management
```bash
# Inside screen (Ctrl+a as prefix)
Ctrl+a d                   # Detach current session
Ctrl+a D D                 # Detach and logout
Ctrl+a \                   # Kill all windows and terminate
Ctrl+a k                   # Kill current window
Ctrl+a ?                   # Show help screen
```

## Window Management

### Creating and Closing Windows
```bash
# Window creation
Ctrl+a c                   # Create new window
Ctrl+a A                   # Rename current window
Ctrl+a k                   # Kill current window
Ctrl+a K                   # Kill current window with notification
Ctrl+a \                   # Kill all windows and quit

# Window selection
Ctrl+a [0-9]              # Switch to window 0-9
Ctrl+a ' [number]         # Switch to window by number
Ctrl+a ' [title]          # Switch to window by title
```

### Window Navigation
```bash
# Navigation commands
Ctrl+a n                   # Next window
Ctrl+a p                   # Previous window
Ctrl+a Ctrl+a             # Toggle between windows
Ctrl+a "                   # List all windows
Ctrl+a w                   # Show window list bar
```

## Screen Navigation

### Basic Movement
```bash
# Scrolling
Ctrl+a [                   # Enter copy mode
Ctrl+a ]                   # Paste copied text
Ctrl+a Esc                 # Enter copy mode (alternate)

# In copy mode
h, j, k, l                # Vim-style movement
Arrow keys                # Move cursor
Ctrl+b                    # Page up
Ctrl+f                    # Page down
0                        # Start of line
$                        # End of line
```

### Search
```bash
# Search in copy mode
/                        # Forward search
?                        # Backward search
n                        # Next occurrence
N                        # Previous occurrence
```

## Split Screen

### Split Management
```bash
# Split commands
Ctrl+a S                   # Split horizontal
Ctrl+a |                   # Split vertical
Ctrl+a Tab                 # Switch between regions
Ctrl+a Q                   # Close all regions except current
Ctrl+a X                   # Close current region

# Region sizing
Ctrl+a :resize +N          # Increase region size by N
Ctrl+a :resize -N          # Decrease region size by N
Ctrl+a :resize =           # Make regions equal size
```

### Split Navigation
```bash
# Moving between splits
Ctrl+a Tab                 # Move to next region
Ctrl+a :focus             # Move to next region (alternate)
Ctrl+a :remove            # Remove current region
```

## Copy and Paste

### Basic Copy Mode
```bash
# Entering copy mode
Ctrl+a [                   # Enter copy mode
Space                     # Start selection
Space                     # End selection

# Pasting
Ctrl+a ]                   # Paste copied text
```

### Advanced Copy Operations
```bash
# Copy mode commands
Ctrl+a a                   # Start/end selection
Ctrl+a >                   # Write buffer to file
Ctrl+a <                   # Read file to buffer
```

## Screen Configuration

### Basic Configuration
```bash
# Create or edit ~/.screenrc
# Sample configurations:

# Display settings
hardstatus alwayslastline
hardstatus string '%{= kG}[ %{G}%H %{g}][%= %{= kw}%?%-Lw%?%{r}(%{W}%n*%f%t%?(%u)%?%{r})%{w}%?%+Lw%?%?%= %{g}][%{B} %m-%d %{W}%c %{g}]'

# Scrollback buffer
defscrollback 10000

# No welcome message
startup_message off

# Enable mouse scrolling
termcapinfo xterm* ti@:te@
```

### Advanced Configuration
```bash
# Window settings
screen -t shell1 0
screen -t shell2 1
screen -t logs 2 tail -f /var/log/syslog

# Key bindings
bindkey -k k1 select 1
bindkey -k k2 select 2
```

## Advanced Features

### Multi-user Support
```bash
# Multi-user commands
screen -x                  # Shared session
screen -m                  # Force creation of new session
Ctrl+a :multiuser on       # Enable multi-user mode
Ctrl+a :acladd [user]      # Add user access
```

### Logging
```bash
# Session logging
Ctrl+a H                   # Toggle logging
screen -L                  # Start with logging enabled
screen -T xterm-256color   # Specify terminal type
```

### Command Execution
```bash
# Remote execution
screen -S session -X stuff "command^M"
screen -S session -X eval "stuff 'command'^M"
```

## Best Practices

1. **Session Management**
   ```bash
   # Always name sessions descriptively
   screen -S project-backend
   screen -S logs-monitoring
   
   # Check existing sessions before creating new ones
   screen -ls
   ```

2. **Window Organization**
   ```bash
   # Use meaningful window names
   Ctrl+a A "server"
   Ctrl+a A "logs"
   Ctrl+a A "shell"
   ```

3. **Configuration Tips**
   - Keep a backup of your .screenrc
   - Document custom key bindings
   - Use consistent naming conventions
   - Set appropriate scrollback size

4. **Security Considerations**
   ```bash
   # Secure multi-user setup
   multiuser on
   acladd [username]
   aclchg [username] +rwx "#?"
   ```

## Troubleshooting

### Common Issues
```bash
# Screen session lost
screen -ls | grep Dead    # Find dead sessions
screen -wipe             # Clean up dead sessions

# Terminal issues
screen -R -DD           # Force reattach
```

## Related Documentation
- [Terminal Management](terminal-management.md)
- [Process Management](process-management.md)
- [System Administration](system-management.md)

---

For more detailed information, use the built-in help:
```bash
Ctrl+a ?                   # Show help screen
man screen                # Screen manual
```