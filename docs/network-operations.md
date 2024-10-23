# Network Operations in Linux

A comprehensive guide for managing network operations, configurations, and troubleshooting in Linux systems.

## Table of Contents
- [Basic Network Commands](#basic-network-commands)
- [Network Configuration](#network-configuration)
- [Network Diagnostics](#network-diagnostics)
- [Network Monitoring](#network-monitoring)
- [Firewall Management](#firewall-management)
- [Network Services](#network-services)
- [Wireless Networking](#wireless-networking)
- [Advanced Networking](#advanced-networking)

## Basic Network Commands

### Network Status
```bash
# Interface information
ip addr show                # Show all interfaces
ip link show               # Show link status
ifconfig                   # Traditional interface info
iwconfig                   # Wireless interface info

# Connection testing
ping [host]               # Test connectivity
ping -c 4 [host]          # Ping 4 times only
ping6 [ipv6-host]         # Test IPv6 connectivity
```

### Network Statistics
```bash
# Connection information
netstat -tuln             # Show listening ports
netstat -anp              # All connections with PID
ss -tuln                  # Socket statistics
ss -anp                   # All connections with PID

# Network statistics
nstat                     # Network statistics
ip -s link               # Interface statistics
```

## Network Configuration

### Interface Management
```bash
# Interface control
ip link set [interface] up     # Enable interface
ip link set [interface] down   # Disable interface
ip addr add [ip]/[mask] dev [interface]  # Add IP
ip addr del [ip]/[mask] dev [interface]  # Remove IP

# DNS configuration
cat /etc/resolv.conf          # View DNS settings
resolvectl status            # SystemD resolver status
```

### Static IP Configuration
```bash
# /etc/network/interfaces example
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
```

### DHCP Configuration
```bash
# Enable DHCP
auto eth0
iface eth0 inet dhcp

# DHCP client commands
dhclient [interface]         # Request new lease
dhclient -r [interface]      # Release DHCP lease
```

## Network Diagnostics

### Connection Testing
```bash
# Basic diagnostics
ping [host]                 # Test connectivity
traceroute [host]           # Show route to host
mtr [host]                  # Combined trace and ping
host [domain]               # DNS lookup
dig [domain]                # Detailed DNS lookup
nslookup [domain]           # Name server lookup
```

### Port Scanning
```bash
# Port checking
nc -zv [host] [port]        # Check specific port
nmap [host]                 # Port scan
nmap -sV [host]             # Service version scan
lsof -i                     # List open ports/connections
```

### Network Troubleshooting
```bash
# Troubleshooting commands
ip route show               # Show routing table
ip neigh show              # Show ARP cache
tcpdump -i [interface]      # Capture packets
tcpdump -i any port 80     # Capture HTTP traffic
arp -a                     # Show ARP table
```

## Network Monitoring

### Traffic Monitoring
```bash
# Traffic monitoring tools
iftop                      # Network traffic monitor
nethogs                    # Per-process bandwidth
iptraf-ng                 # Interactive traffic monitor
bmon                      # Bandwidth monitor
```

### Network Analysis
```bash
# Detailed analysis
wireshark                  # GUI packet analyzer
tshark                    # CLI packet analyzer
nload                     # Network load monitor
vnstat                    # Traffic statistics
```

## Firewall Management

### UFW (Uncomplicated Firewall)
```bash
# Basic UFW commands
ufw enable                 # Enable firewall
ufw disable                # Disable firewall
ufw status                 # Show firewall status
ufw allow [port/service]   # Allow port
ufw deny [port/service]    # Deny port
ufw delete [rule]          # Remove rule
```

### IPTables
```bash
# IPTables commands
iptables -L               # List all rules
iptables -A INPUT -p tcp --dport 80 -j ACCEPT  # Allow HTTP
iptables -A INPUT -j DROP # Drop all other traffic
iptables-save            # Save rules
iptables-restore        # Restore rules
```

## Network Services

### SSH Configuration
```bash
# SSH service management
systemctl status ssh      # Check SSH status
systemctl start ssh      # Start SSH service
systemctl enable ssh     # Enable at boot

# SSH client commands
ssh [user]@[host]        # Connect to host
ssh -p [port] [user]@[host]  # Connect to specific port
ssh-keygen              # Generate SSH keys
ssh-copy-id [user]@[host]   # Copy SSH key to server
```

### Web Server
```bash
# Apache management
systemctl status apache2  # Check Apache status
apache2ctl -t            # Test configuration
apache2ctl -S            # Show virtual hosts

# Nginx management
systemctl status nginx   # Check Nginx status
nginx -t                # Test configuration
nginx -s reload         # Reload configuration
```

## Wireless Networking

### Wireless Tools
```bash
# Network scanning
iwlist [interface] scan   # Scan for networks
nmcli dev wifi           # List available networks
nmcli dev wifi connect [SSID] password [password]  # Connect

# Network management
nmtui                    # Text UI for NetworkManager
nm-connection-editor     # GUI network editor
```

## Advanced Networking

### Network Bridging
```bash
# Create bridge
ip link add name br0 type bridge
ip link set dev br0 up
ip link set dev [interface] master br0

# Delete bridge
ip link set dev [interface] nomaster
ip link delete br0 type bridge
```

### VLAN Configuration
```bash
# Create VLAN
ip link add link [interface] name [interface].[vlan-id] type vlan id [vlan-id]
ip link set dev [interface].[vlan-id] up

# Delete VLAN
ip link delete [interface].[vlan-id]
```

## Best Practices

1. **Security**
   - Regularly update firewall rules
   - Monitor network traffic
   - Use secure protocols (SSH, HTTPS)
   - Implement network segmentation

2. **Performance**
   - Monitor bandwidth usage
   - Optimize network configurations
   - Use appropriate MTU settings
   - Implement QoS when needed

3. **Maintenance**
   - Regular security updates
   - Monitor system logs
   - Document network changes
   - Backup configurations

4. **Troubleshooting**
   - Check physical connections
   - Verify IP configuration
   - Test DNS resolution
   - Monitor error logs

## Related Documentation
- [System Management](system-management.md)
- [Security Practices](security-practices.md)
- [SSH Advanced Guide](ssh-advanced.md)

---

For more detailed information about specific commands, use the `man` command:
```bash
man ip
man netstat
man tcpdump
```