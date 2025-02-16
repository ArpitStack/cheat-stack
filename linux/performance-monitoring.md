# Linux Performance Monitoring CheatSheet

A practical guide covering essential Linux commands for monitoring and optimizing system performance.

## Table of Contents

- [CPU Monitoring](#cpu-monitoring)
- [Memory Usage](#memory-usage)
- [Disk Usage & I/O](#disk-usage--io)
- [Network Performance](#network-performance)
- [Process Monitoring](#process-monitoring)
- [System Load & Uptime](#system-load--uptime)
- [Logging & Debugging](#logging--debugging)

## CPU Monitoring

Check CPU usage:

```bash
mpstat 1 5  # Requires sysstat package
```

View CPU-intensive processes:

```bash
top  # Press 'q' to exit
htop  # Requires installation, more user-friendly
```

Check CPU load average:

```bash
uptime
cat /proc/loadavg
```

## Memory Usage

Check memory usage:

```bash
free -h
```

View memory details:

```bash
vmstat 1 5
```

Check memory-intensive processes:

```bash
top -o %MEM
```

## Disk Usage & I/O

Check disk space:

```bash
df -h
```

Check disk usage per directory:

```bash
du -sh *
```

Monitor disk I/O:

```bash
iostat -x 1 5  # Requires sysstat package
```

View disk activity:

```bash
iotop  # Requires installation
```

## Network Performance

Check active network connections:

```bash
ss -tulnp
```

Monitor real-time network traffic:

```bash
iftop  # Requires installation
```

Test network bandwidth:

```bash
iperf3 -s  # Start server
iperf3 -c <server-ip>  # Run client
```

## Process Monitoring

List running processes:

```bash
ps aux
```

Find a specific process:

```bash
ps aux | grep <process-name>
```

Kill a process by PID:

```bash
kill <PID>
```

Force kill a process:

```bash
kill -9 <PID>
```

## System Load & Uptime

Check system uptime:

```bash
uptime
```

View system load average:

```bash
cat /proc/loadavg
```

## Logging & Debugging

View system logs:

```bash
journalctl -xe
```

Check kernel logs:

```bash
dmesg | tail -50
```

Monitor logs in real-time:

```bash
tail -f /var/log/syslog
```