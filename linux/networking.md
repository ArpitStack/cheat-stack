# Linux Networking Commands CheatSheet

A practical guide covering essential Linux networking commands for troubleshooting, configuration, and daily operations.

## Table of Contents

- [Check Network Interfaces](#check-network-interfaces)
- [IP Address & Routing](#ip-address--routing)
- [DNS & Hostname](#dns--hostname)
- [Network Connectivity](#network-connectivity)
- [Firewall & Security](#firewall--security)
- [Packet Analysis](#packet-analysis)
- [Network Services](#network-services)
- [Port Management](#port-management)

## Check Network Interfaces

List all network interfaces:

```bash
ip a
ifconfig  # Deprecated, but still available in some distros
```

Check active connections:

```bash
ss -tulnp  # More modern alternative to netstat
netstat -tulnp  # Requires net-tools package
```

## IP Address & Routing

Get IP address of system:

```bash
hostname -I
ip a show eth0
```

Add an IP address:

```bash
sudo ip addr add 192.168.1.100/24 dev eth0
```

View routing table:

```bash
ip route show
default via 192.168.1.1 dev eth0
```

Add a static route:

```bash
sudo ip route add 10.10.10.0/24 via 192.168.1.1 dev eth0
```

## DNS & Hostname

Check system hostname:

```bash
hostnamectl
```

Set system hostname:

```bash
sudo hostnamectl set-hostname new-hostname
```

Test DNS resolution:

```bash
dig google.com  # Requires dnsutils package
nslookup google.com
host google.com
```

## Network Connectivity

Check connectivity:

```bash
ping -c 4 google.com
```

Check open ports on remote server:

```bash
nc -zv google.com 80
```

Trace network route:

```bash
traceroute google.com  # Requires traceroute package
```

## Firewall & Security

Check firewall rules (UFW):

```bash
sudo ufw status
```

Allow incoming SSH connections:

```bash
sudo ufw allow 22/tcp
```

Enable firewall:

```bash
sudo ufw enable
```

For iptables:

```bash
sudo iptables -L -v -n
```

## Packet Analysis

Capture network packets:

```bash
sudo tcpdump -i eth0 port 80
```

Save captured packets to a file:

```bash
sudo tcpdump -i eth0 -w capture.pcap
```

Analyze packet capture:

```bash
tshark -r capture.pcap  # Requires Wireshark/tshark
```

## Network Services

Restart networking service:

```bash
sudo systemctl restart networking
```

Check if a network service is running:

```bash
sudo systemctl status networking
```

## Port Management

Check open ports:

```bash
netstat -tulnp
ss -tulnp  # Modern alternative
```

Test if a port is open:

```bash
nc -zv 192.168.1.1 80
```

Kill a process using a specific port:

```bash
sudo fuser -k 80/tcp
```
