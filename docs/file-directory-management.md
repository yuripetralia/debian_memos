# File and Directory Management in Linux

This guide covers essential commands and techniques for managing files and directories in Linux systems.

## Table of Contents
- [Basic Navigation](#basic-navigation)
- [File Operations](#file-operations)
- [Directory Operations](#directory-operations)
- [Permission Management](#permission-management)
- [File Search and Location](#file-search-and-location)
- [File Information](#file-information)
- [Advanced Operations](#advanced-operations)
- [Best Practices](#best-practices)

## Basic Navigation

### Essential Navigation Commands
```bash
# List directory contents
ls                    # Basic listing
ls -l                 # Detailed listing
ls -la                # Include hidden files
ls -lh                # Human-readable file sizes
ls -lR                # Recursive listing
ls -lt                # Sort by modification time
ls -lS                # Sort by file size

# Change directory
cd [directory]        # Change to specific directory
cd                    # Change to home directory
cd ~                  # Change to home directory
cd -                  # Change to previous directory
cd ..                 # Move up one directory
cd ../../            # Move up two directories

# Print working directory
pwd                   # Show current directory path
pwd -P                # Show physical path (resolve symlinks)
```

## File Operations

### Basic File Operations
```bash
# Create files
touch [filename]      # Create empty file or update timestamp
touch file{1..10}.txt # Create multiple files

# Copy files
cp [source] [dest]    # Copy file
cp -r [source] [dest] # Copy directory recursively
cp -p [source] [dest] # Preserve attributes
cp -i [source] [dest] # Interactive mode (prompt before overwrite)

# Move/rename files
mv [source] [dest]    # Move or rename file
mv -i [source] [dest] # Interactive mode
mv -u [source] [dest] # Update (move only newer files)

# Delete files
rm [file]            # Remove file
rm -f [file]         # Force remove
rm -i [file]         # Interactive mode
rm -r [directory]    # Remove directory and contents
```

## Directory Operations

### Managing Directories
```bash
# Create directories
mkdir [name]         # Create directory
mkdir -p [path]      # Create parent directories as needed
mkdir -m 755 [name]  # Create with specific permissions

# Remove directories
rmdir [directory]    # Remove empty directory
rm -r [directory]    # Remove directory and contents
rm -rf [directory]   # Force remove directory and contents

# Copy directories
cp -r [source] [dest] # Copy directory recursively
cp -a [source] [dest] # Archive mode (preserve attributes)
```

## Permission Management

### File Permissions
```bash
# Change permissions
chmod [permissions] [file]  # Change file mode
chmod 755 [file]           # Set specific permissions
chmod +x [file]            # Add execute permission
chmod -w [file]            # Remove write permission
chmod -R [permissions] [directory]  # Recursive change

# Change ownership
chown [user]:[group] [file]     # Change owner and group
chown -R [user] [directory]     # Recursive ownership change
chgrp [group] [file]            # Change group ownership
```

### Understanding Permissions
```bash
# Permission structure
# rwx rwx rwx = user group others
# 421 421 421 = numeric values

# Common permission sets
chmod 777 [file]  # rwxrwxrwx (full access)
chmod 755 [file]  # rwxr-xr-x (standard executable)
chmod 644 [file]  # rw-r--r-- (standard file)
chmod 600 [file]  # rw------- (private file)
```

## File Search and Location

### Finding Files
```bash
# Find commands
find [path] -name [pattern]     # Find by name
find [path] -type f             # Find files
find [path] -type d             # Find directories
find [path] -mtime +/-n         # Find by modification time
find [path] -size +/-n          # Find by size
find [path] -perm [mode]        # Find by permissions

# Examples
find . -name "*.txt"            # Find all .txt files
find . -type f -mtime -7        # Files modified in last 7 days
find . -size +100M              # Files larger than 100MB
```

### Location Commands
```bash
# Locate command (requires updatedb)
updatedb                    # Update file database
locate [pattern]           # Find files by pattern
locate -i [pattern]        # Case-insensitive search

# Which command
which [command]            # Show command location
whereis [command]          # Show binary, source, manual locations
```

## File Information

### Viewing File Details
```bash
# File information
file [file]               # Show file type
stat [file]              # Show file status
wc [file]                # Count lines, words, chars

# File content
cat [file]               # Display file content
less [file]              # Page through file
head [file]              # Show first 10 lines
tail [file]              # Show last 10 lines
tail -f [file]           # Follow file changes
```

## Advanced Operations

### Symbolic Links
```bash
# Create symbolic links
ln -s [target] [link]    # Create symbolic link
ln [target] [link]       # Create hard link

# Update links
ln -sf [target] [link]   # Force update symbolic link
```

### Batch Operations
```bash
# Batch rename
rename 's/old/new/' files*    # Rename using pattern

# Batch operations with find
find . -name "*.txt" -exec chmod 644 {} \;
find . -name "*.sh" -exec chmod +x {} \;
```

## Best Practices

1. **File Organization**
   - Use meaningful names for files and directories
   - Maintain consistent naming conventions
   - Keep related files together
   - Use appropriate file extensions

2. **Permission Management**
   - Apply principle of least privilege
   - Regularly audit permissions
   - Use groups for shared access
   - Be careful with recursive permission changes

3. **Safety Measures**
   ```bash
   # Use interactive mode for critical operations
   cp -i
   mv -i
   rm -i

   # Make backup copies of important files
   cp file{,.bak}

   # Use safe rm alternatives
   trash-put [file]  # Instead of rm
   ```

4. **Directory Structure**
   - Follow Filesystem Hierarchy Standard (FHS)
   - Keep user data in home directory
   - Use appropriate temporary directories
   - Maintain clean root directory

## Related Documentation
- [Package Management](package-management.md)
- [System Management](system-management.md)
- [Text Processing](text-processing.md)

---

For more detailed information about specific commands, use the `man` command:
```bash
man ls
man chmod
man find
```