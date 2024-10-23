# Compression Tools in Linux

A comprehensive guide for file compression, archiving, and management in Linux systems.

## Table of Contents
- [Basic Compression Tools](#basic-compression-tools)
- [Archive Management](#archive-management)
- [Advanced Compression](#advanced-compression)
- [Specialized Tools](#specialized-tools)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Basic Compression Tools

### Gzip (.gz)
```bash
# Compression
gzip [file]                # Compress file
gzip -k [file]             # Keep original file
gzip -9 [file]             # Best compression
gzip -1 [file]             # Fastest compression

# Decompression
gunzip [file.gz]           # Decompress file
gzip -d [file.gz]          # Decompress file
zcat [file.gz]             # View compressed file

# Multiple files
gzip [file1] [file2]       # Compress multiple files
gzip -r [directory]        # Recursive compression
```

### Bzip2 (.bz2)
```bash
# Compression
bzip2 [file]               # Compress file
bzip2 -k [file]            # Keep original file
bzip2 -9 [file]            # Best compression
bzip2 -1 [file]            # Fastest compression

# Decompression
bunzip2 [file.bz2]         # Decompress file
bzip2 -d [file.bz2]        # Decompress file
bzcat [file.bz2]           # View compressed file

# Multiple files
bzip2 [file1] [file2]      # Compress multiple files
```

### XZ (.xz)
```bash
# Compression
xz [file]                  # Compress file
xz -k [file]               # Keep original file
xz -9 [file]               # Best compression
xz -0 [file]               # Fastest compression

# Decompression
unxz [file.xz]             # Decompress file
xz -d [file.xz]            # Decompress file
xzcat [file.xz]            # View compressed file
```

## Archive Management

### Tar Archives
```bash
# Creating archives
tar -cf [archive.tar] [files]     # Create archive
tar -czf [archive.tar.gz] [files] # Create gzipped archive
tar -cjf [archive.tar.bz2] [files]# Create bzip2 archive
tar -cJf [archive.tar.xz] [files] # Create xz archive

# Extracting archives
tar -xf [archive.tar]             # Extract archive
tar -xzf [archive.tar.gz]         # Extract gzipped archive
tar -xjf [archive.tar.bz2]        # Extract bzip2 archive
tar -xJf [archive.tar.xz]         # Extract xz archive

# Additional options
tar -tvf [archive]                # List contents
tar -C [directory] -xf [archive]  # Extract to directory
tar --exclude=[pattern] -czf [archive] [files]  # Exclude files
```

### ZIP Archives
```bash
# Creating ZIP archives
zip [archive.zip] [files]         # Create archive
zip -r [archive.zip] [directory]  # Recursive archive
zip -e [archive.zip] [files]      # Encrypted archive
zip -9 [archive.zip] [files]      # Best compression

# Extracting ZIP archives
unzip [archive.zip]               # Extract archive
unzip -l [archive.zip]            # List contents
unzip -d [directory] [archive.zip]# Extract to directory
unzip -P [password] [archive.zip] # Extract encrypted
```

### RAR Archives
```bash
# Creating RAR archives (if rar is installed)
rar a [archive.rar] [files]       # Create archive
rar a -r [archive.rar] [directory]# Recursive archive
rar a -p [archive.rar] [files]    # Encrypted archive

# Extracting RAR archives
unrar x [archive.rar]             # Extract archive
unrar l [archive.rar]             # List contents
unrar t [archive.rar]             # Test archive
```

## Advanced Compression

### 7-Zip (.7z)
```bash
# Creating 7z archives
7z a [archive.7z] [files]         # Create archive
7z a -t7z -m0=lzma2 -mx=9 [archive.7z] [files]  # Best compression
7z a -p [archive.7z] [files]      # Encrypted archive

# Extracting 7z archives
7z x [archive.7z]                 # Extract archive
7z l [archive.7z]                 # List contents
7z t [archive.7z]                 # Test archive
```

### Compression with Filters
```bash
# Using pipes for compression
tar cf - [files] | gzip -9 > [archive.tar.gz]
tar cf - [files] | xz -9 > [archive.tar.xz]

# Parallel compression
tar cf - [files] | pigz > [archive.tar.gz]
tar cf - [files] | pbzip2 > [archive.tar.bz2]
```

## Specialized Tools

### File Splitting
```bash
# Split large files
split -b 1G [file] [prefix]       # Split by size
split -n [number] [file] [prefix] # Split into parts

# Combine split files
cat [prefix]* > [file]            # Combine parts
```

### Archive Verification
```bash
# Verify archives
tar -tvf [archive.tar]            # Test tar archive
gzip -t [file.gz]                 # Test gzip file
bzip2 -t [file.bz2]               # Test bzip2 file
unzip -t [archive.zip]            # Test ZIP archive
```

### Backup Tools
```bash
# Backup with compression
rsync -az [source] [destination]  # Compressed sync
dd if=[source] | gzip > [backup.gz] # Disk image backup
```

## Best Practices

1. **Choosing Compression Methods**
   ```bash
   # For best compression ratio
   xz -9 [file]
   7z a -t7z -m0=lzma2 -mx=9 [archive.7z] [files]

   # For faster compression
   gzip -1 [file]
   zip -0 [archive.zip] [files]

   # For balanced compression
   gzip -6 [file]
   ```

2. **Archive Management**
   - Keep original files until verifying archives
   - Use appropriate compression for file types
   - Document archive contents
   - Test archives after creation

3. **Resource Considerations**
   ```bash
   # Memory efficient
   nice -n 19 gzip -1 [file]      # Low priority, fast
   
   # CPU efficient
   xz --threads=0 [file]          # Use all cores
   ```

4. **Security Practices**
   ```bash
   # Encrypted archives
   zip -e [archive.zip] [files]
   7z a -p[password] [archive.7z] [files]
   
   # Secure deletion
   shred -u [original-file]
   ```

## Troubleshooting

### Common Issues
```bash
# Corrupted archives
gzip -tv [file.gz]               # Test gzip file
bzip2 recover [file.bz2]         # Recover bzip2
zip -FF [broken.zip] --out [fixed.zip]  # Fix ZIP

# Space issues
du -sh [directory]               # Check space usage
df -h                           # Check disk space
```

### Recovery Options
```bash
# Recover damaged archives
tar --ignore-zeros -xf [archive.tar]    # Ignore errors
7z x -y [archive.7z]                    # Force extraction
unzip -FF [archive.zip]                 # Fix ZIP archive
```

## Related Documentation
- [File Management](file-directory-management.md)
- [Backup Strategies](backup-strategies.md)
- [Storage Management](storage-management.md)

---

For more detailed information about specific commands, use the `man` command:
```bash
man tar
man gzip
man zip
```