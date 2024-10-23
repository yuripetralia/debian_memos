# Text Processing in Linux

A comprehensive guide for text processing, manipulation, and analysis in Linux systems.

## Table of Contents
- [Basic Text Commands](#basic-text-commands)
- [Text Viewing and Navigation](#text-viewing-and-navigation)
- [Text Analysis](#text-analysis)
- [Text Manipulation](#text-manipulation)
- [Pattern Matching](#pattern-matching)
- [Stream Processing](#stream-processing)
- [Advanced Text Processing](#advanced-text-processing)
- [Best Practices](#best-practices)

## Basic Text Commands

### File Display
```bash
# Display commands
cat [file]               # Display entire file
less [file]             # Page through file
more [file]             # Simple pager
head [file]             # Show first 10 lines
head -n [N] [file]      # Show first N lines
tail [file]             # Show last 10 lines
tail -n [N] [file]      # Show last N lines
tail -f [file]          # Follow file changes
```

### Basic Text Analysis
```bash
# Word, line, character counting
wc [file]               # Word, line, char count
wc -l [file]            # Count lines
wc -w [file]            # Count words
wc -c [file]            # Count bytes
wc -m [file]            # Count characters
```

## Text Viewing and Navigation

### File Navigation
```bash
# less commands
less [file]
    /pattern           # Search forward
    ?pattern           # Search backward
    n                 # Next occurrence
    N                 # Previous occurrence
    g                 # Go to first line
    G                 # Go to last line
    q                 # Quit
    
# more commands
more [file]
    Space             # Next page
    Enter             # Next line
    q                 # Quit
```

### Multiple File Viewing
```bash
# Compare files
diff [file1] [file2]    # Show differences
diff -u [file1] [file2] # Unified format
sdiff [file1] [file2]   # Side-by-side diff
vimdiff [file1] [file2] # Visual diff in vim
```

## Text Analysis

### Pattern Search
```bash
# grep commands
grep [pattern] [file]        # Search for pattern
grep -i [pattern] [file]     # Case-insensitive search
grep -r [pattern] [dir]      # Recursive search
grep -v [pattern] [file]     # Invert match
grep -c [pattern] [file]     # Count matches
grep -n [pattern] [file]     # Show line numbers
grep -l [pattern] [files]    # List matching files

# Advanced grep
grep -E [regex] [file]       # Extended regex
grep -P [regex] [file]       # Perl regex
grep -w [word] [file]        # Match whole words
grep -A [N] [pattern] [file] # N lines after match
grep -B [N] [pattern] [file] # N lines before match
```

### Text Statistics
```bash
# Text analysis
sort [file]                  # Sort lines
sort -n [file]              # Numeric sort
sort -r [file]              # Reverse sort
sort -u [file]              # Sort and remove duplicates
uniq [file]                 # Remove adjacent duplicates
uniq -c [file]              # Count occurrences
uniq -d [file]              # Show only duplicates
```

## Text Manipulation

### Basic Manipulation
```bash
# Text transformation
tr [set1] [set2]            # Translate characters
tr -d [chars]               # Delete characters
tr -s [chars]               # Squeeze repeats
cut -d[delim] -f[N] [file]  # Cut by delimiter
cut -c[N-M] [file]          # Cut by characters

# Line manipulation
paste [file1] [file2]       # Merge lines
join [file1] [file2]        # Join on common field
expand [file]               # Convert tabs to spaces
unexpand [file]             # Convert spaces to tabs
```

### Advanced Manipulation
```bash
# sed commands
sed 's/old/new/' [file]     # Replace first occurrence
sed 's/old/new/g' [file]    # Replace all occurrences
sed -i 's/old/new/g' [file] # Replace in file
sed 'Nd' [file]             # Delete line N
sed '/pattern/d' [file]     # Delete matching lines

# awk processing
awk '{print $1}' [file]     # Print first field
awk -F: '{print $1}' [file] # Custom delimiter
awk 'NR==1' [file]          # Print first line
awk 'length>80' [file]      # Lines longer than 80
```

## Pattern Matching

### Regular Expressions
```bash
# Basic patterns
.                   # Any single character
^                   # Start of line
$                   # End of line
*                   # Zero or more
+                   # One or more
?                   # Zero or one
[]                  # Character class
[^]                 # Negated character class

# Extended patterns
\w                  # Word character
\W                  # Non-word character
\d                  # Digit
\D                  # Non-digit
\s                  # Whitespace
\S                  # Non-whitespace
```

### Pattern Examples
```bash
# Common patterns
grep '^[0-9]' [file]        # Lines starting with number
grep '[A-Za-z]$' [file]     # Lines ending with letter
grep '^$' [file]            # Empty lines
grep '^\s*$' [file]         # Blank lines
grep -E '\b\w{6}\b' [file]  # Six-letter words
```

## Stream Processing

### Pipelines
```bash
# Common pipelines
cat [file] | grep [pattern] | sort | uniq -c    # Count unique matches
tail -f [log] | grep --line-buffered [pattern]  # Monitor filtered log
cut -d: -f1 [file] | sort | uniq -c            # Count field occurrences
```

### Process Substitution
```bash
# Compare sorted files
comm <(sort file1) <(sort file2)
# Find unique lines
diff <(sort file1) <(sort file2)
```

## Advanced Text Processing

### Text Extraction
```bash
# Extract specific content
grep -oP 'pattern\K.*?(?=end)' [file]  # Extract between patterns
sed -n '/start/,/end/p' [file]         # Print between patterns
awk '/start/,/end/' [file]             # Print between patterns
```

### Text Formatting
```bash
# Format text
fmt [file]                    # Format text
pr [file]                    # Format for printing
fold -w [width] [file]       # Wrap lines
column -t [file]             # Columnate text
```

### Binary File Processing
```bash
# Binary file handling
strings [file]               # Extract text from binary
hexdump -C [file]           # Hex dump
od -c [file]                # Octal dump
xxd [file]                  # Hex editor output
```

## Best Practices

1. **Performance**
   - Use appropriate tools for the task
   - Consider memory usage for large files
   - Use streaming where possible
   - Optimize regular expressions

2. **Data Handling**
   - Make backups before modification
   - Test commands on sample data
   - Use version control
   - Document complex text processing

3. **Script Development**
   - Comment complex patterns
   - Use meaningful variable names
   - Break complex operations into steps
   - Test edge cases

4. **File Management**
   - Use appropriate file permissions
   - Keep backups of important files
   - Use proper character encoding
   - Handle large files appropriately

## Related Documentation
- [File Management](file-directory-management.md)
- [Shell Scripting](shell-scripting.md)
- [System Administration](system-management.md)

---

For more detailed information about specific commands, use the `man` command:
```bash
man grep
man sed
man awk
```