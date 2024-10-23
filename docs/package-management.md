# Package Management in Debian Linux

This guide covers the essential package management commands and best practices for Debian-based Linux systems using the Advanced Package Tool (APT).

## Table of Contents
- [Basic APT Commands](#basic-apt-commands)
- [Package Search and Information](#package-search-and-information)
- [Package Installation and Removal](#package-installation-and-removal)
- [System Updates](#system-updates)
- [Advanced APT Usage](#advanced-apt-usage)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Basic APT Commands

### Essential Commands
```bash
# Update package list
apt update

# Upgrade installed packages
apt upgrade

# Full system upgrade (may remove packages)
apt full-upgrade

# Install a package
apt install [package]

# Remove a package
apt remove [package]

# Remove package and configuration files
apt purge [package]

# Remove unnecessary packages
apt autoremove
```

### Package Search and Information
```bash
# Search for packages
apt search [term]

# Show package details
apt show [package]

# List all packages matching a pattern
apt list [pattern]

# Show package dependencies
apt depends [package]
```

## Package Installation and Removal

### Installation Options
```bash
# Install without recommends
apt install --no-install-recommends [package]

# Install specific version
apt install [package]=[version]

# Install multiple packages
apt install [package1] [package2]

# Install without asking for confirmation
apt install -y [package]
```

### Removal Options
```bash
# Remove package but keep configuration
apt remove [package]

# Remove package and configuration
apt purge [package]

# Remove automatically installed dependencies
apt autoremove

# Remove downloaded package files
apt clean
```

## System Updates

### Update Process
```bash
# Update package lists
apt update

# Show upgradeable packages
apt list --upgradable

# Perform safe upgrade
apt upgrade

# Perform full upgrade
apt full-upgrade
```

### Automatic Updates
To configure automatic updates:
1. Install the unattended-upgrades package:
```bash
apt install unattended-upgrades
```

2. Configure automatic updates:
```bash
dpkg-reconfigure -plow unattended-upgrades
```

## Advanced APT Usage

### Package Holding
```bash
# Prevent package from being upgraded
apt-mark hold [package]

# Remove upgrade hold
apt-mark unhold [package]

# Show held packages
apt-mark showhold
```

### Package Download
```bash
# Download without installing
apt download [package]

# Get source package
apt source [package]

# Download package and dependencies
apt install --download-only [package]
```

### Repository Management
```bash
# Add repository
add-apt-repository [repository]

# Remove repository
add-apt-repository --remove [repository]
```

## Best Practices

1. **Regular Updates**
   - Update package lists daily
   - Perform system upgrades regularly
   - Review upgrade changes before applying

2. **Package Management**
   - Keep track of manually installed packages
   - Regularly remove unnecessary packages
   - Maintain a list of essential packages

3. **Security**
   - Enable security updates
   - Configure automatic security upgrades
   - Monitor package authentication

4. **System Maintenance**
   ```bash
   # Regular maintenance commands
   apt update
   apt upgrade
   apt autoremove
   apt clean
   ```

## Troubleshooting

### Common Issues and Solutions

1. **Locked Database**
```bash
# Error: Could not get lock /var/lib/dpkg/lock
# Solution:
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock*
sudo dpkg --configure -a
```

2. **Broken Packages**
```bash
# Fix broken packages
apt --fix-broken install

# Reconfigure packages
dpkg --configure -a
```

3. **Failed Updates**
```bash
# Clean package cache
apt clean
apt autoclean

# Update package lists
apt update --fix-missing
```

### Verification Commands
```bash
# Verify package integrity
apt-cache verify [package]

# Check for broken dependencies
apt-get check

# Verify installed packages
dpkg -C
```

## Related Documentation
- [System Management](system-management.md)
- [Security Best Practices](security-practices.md)
- [Repository Configuration](repository-config.md)

---

For more detailed information about specific commands, use the `man` command:
```bash
man apt
man apt-get
man dpkg
```