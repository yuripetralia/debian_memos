# Advanced SSH Guide for Linux

A comprehensive guide for advanced SSH configurations, tunneling, security, and management.

## Table of Contents
- [Basic SSH Configuration](#basic-ssh-configuration)
- [Key Management](#key-management)
- [Connection Management](#connection-management)
- [Port Forwarding](#port-forwarding)
- [Jump Hosts](#jump-hosts)
- [Security Hardening](#security-hardening)
- [Advanced Features](#advanced-features)
- [Troubleshooting](#troubleshooting)

## Basic SSH Configuration

### SSH Client Configuration
```bash
# ~/.ssh/config structure
Host [hostname]
    HostName [ip/domain]
    User [username]
    Port [port]
    IdentityFile ~/.ssh/[key]

# Common configuration examples
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
    
Host server
    HostName 192.168.1.100
    User admin
    Port 2222
    IdentityFile ~/.ssh/server_key
```

### SSH Server Configuration
```bash
# /etc/ssh/sshd_config key settings
Port 22
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys

# Apply changes
systemctl restart sshd
```

## Key Management

### Key Generation
```bash
# Generate new SSH key pair
ssh-keygen -t ed25519 -C "comment"
ssh-keygen -t rsa -b 4096 -C "comment"

# Generate with specific options
ssh-keygen -t ed25519 -f ~/.ssh/custom_key -C "comment"
ssh-keygen -t rsa -b 4096 -f ~/.ssh/custom_key -N "passphrase"

# Certificate authority key
ssh-keygen -t rsa -b 4096 -f ~/ssh_ca
```

### Key Distribution
```bash
# Copy public key to server
ssh-copy-id user@remote
ssh-copy-id -i ~/.ssh/custom_key.pub user@remote
ssh-copy-id -p 2222 user@remote

# Manual key copy
cat ~/.ssh/id_ed25519.pub | ssh user@remote "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

## Connection Management

### SSH Options
```bash
# Connection options
ssh -o "ConnectTimeout 10" user@remote
ssh -o "ServerAliveInterval 60" user@remote
ssh -o "StrictHostKeyChecking no" user@remote

# Multiple options
ssh -o "Option1=value1" -o "Option2=value2" user@remote
```

### Connection Multiplexing
```bash
# Enable multiplexing in ~/.ssh/config
Host *
    ControlMaster auto
    ControlPath ~/.ssh/control:%h:%p:%r
    ControlPersist 10m

# Manual multiplexing
ssh -M -S ~/.ssh/control:%h:%p:%r user@remote
ssh -S ~/.ssh/control:%h:%p:%r user@remote
```

## Port Forwarding

### Local Port Forwarding
```bash
# Forward local port to remote system
ssh -L local_port:destination_host:destination_port user@remote

# Examples
ssh -L 8080:localhost:80 user@remote          # Web server
ssh -L 3306:localhost:3306 user@remote        # MySQL
ssh -L *:8080:localhost:80 user@remote        # Allow external access

# Multiple forwards
ssh -L 8080:localhost:80 -L 3306:localhost:3306 user@remote
```

### Remote Port Forwarding
```bash
# Forward remote port to local system
ssh -R remote_port:localhost:local_port user@remote

# Examples
ssh -R 8080:localhost:80 user@remote          # Expose local web server
ssh -R 3000:localhost:3000 user@remote        # Expose local service

# GatewayPorts configuration
ssh -R *:8080:localhost:80 user@remote        # Allow remote external access
```

### Dynamic Port Forwarding
```bash
# Create SOCKS proxy
ssh -D local_port user@remote

# Examples
ssh -D 1080 user@remote                       # SOCKS proxy on port 1080
ssh -D 0.0.0.0:1080 user@remote              # Allow external access
```

## Jump Hosts

### ProxyJump Configuration
```bash
# Using ProxyJump command
ssh -J jump_host user@destination

# Multiple jumps
ssh -J user1@jump1,user2@jump2 user@destination

# In ~/.ssh/config
Host destination
    HostName destination_host
    User user
    ProxyJump jump1,jump2
```

### ProxyCommand Configuration
```bash
# Using ProxyCommand
ssh -o ProxyCommand="ssh jump_host nc %h %p" destination

# In ~/.ssh/config
Host destination
    ProxyCommand ssh jump_host nc %h %p
```

## Security Hardening

### Server Configuration
```bash
# /etc/ssh/sshd_config security settings
Protocol 2
PermitRootLogin no
PasswordAuthentication no
PermitEmptyPasswords no
MaxAuthTries 3
ClientAliveInterval 300
ClientAliveCountMax 2
AllowUsers user1 user2
DenyUsers baduser
AllowGroups sshusers
```

### Key Security
```bash
# Secure key permissions
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/config

# Using ssh-agent
eval $(ssh-agent)
ssh-add ~/.ssh/id_rsa
ssh-add -l                                    # List keys
```

## Advanced Features

### X11 Forwarding
```bash
# Enable X11 forwarding
ssh -X user@remote                            # Enable forwarding
ssh -Y user@remote                            # Trusted forwarding

# In ~/.ssh/config
Host *
    ForwardX11 yes
    ForwardX11Trusted yes
```

### SSHFS
```bash
# Mount remote filesystem
sshfs user@remote:/path /local/mount/point
sshfs -o reconnect user@remote:/path /local/mount/point

# Unmount
fusermount -u /local/mount/point
```

### SSH Tunneling
```bash
# Create persistent tunnel
autossh -M 20000 -f -N -L 8080:localhost:80 user@remote

# Reverse tunnel with autossh
autossh -M 20000 -f -N -R 8080:localhost:80 user@remote
```

## Troubleshooting

### Debug Mode
```bash
# Enable verbose output
ssh -v user@remote                            # Verbose
ssh -vv user@remote                           # More verbose
ssh -vvv user@remote                          # Debug level

# Test configuration
ssh -T git@github.com                         # Test GitHub access
ssh -G hostname                               # Test configuration
```

### Common Issues
```bash
# Connection issues
ssh -o ConnectTimeout=10 user@remote          # Timeout issues
ssh -o ServerAliveInterval=60 user@remote     # Keep alive

# Key issues
ssh-add -l                                    # List loaded keys
ssh-add ~/.ssh/id_rsa                        # Add key manually
ssh-keygen -R hostname                        # Remove host key
```

## Best Practices

1. **Key Management**
   - Use strong key types (ED25519 or RSA 4096-bit)
   - Protect private keys with passphrases
   - Regularly rotate keys
   - Use separate keys for different purposes

2. **Security**
   - Disable password authentication
   - Use non-standard ports
   - Implement fail2ban
   - Regular security audits
   - Keep software updated

3. **Performance**
   - Use connection multiplexing
   - Enable compression when needed
   - Configure appropriate timeouts
   - Use persistent connections

4. **Maintenance**
   - Regular backups of SSH configurations
   - Monitor logs for suspicious activity
   - Document custom configurations
   - Test configuration changes

## Related Documentation
- [Network Operations](network-operations.md)
- [Security Best Practices](security-practices.md)
- [System Administration](system-management.md)

---

For more detailed information, use the man command:
```bash
man ssh
man sshd
man ssh_config
man sshd_config
```