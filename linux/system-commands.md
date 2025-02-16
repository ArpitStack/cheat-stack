# Linux System Commands CheatSheet

A practical guide covering essential Linux commands for system management, troubleshooting, and daily operations.

## Table of Contents

- [System Information](#system-information)
- [User Management](#user-management)
- [Process Management](#process-management)
- [Disk Management](#disk-management)
- [File Management](#file-management)
- [Permissions & Ownership](#permissions--ownership)
- [Package Management](#package-management)
- [System Performance & Monitoring](#system-performance--monitoring)
- [Logs & Debugging](#logs--debugging)
- [Archiving & Compression](#archiving--compression)
- [Job Scheduling](#job-scheduling)
- [System Security](#system-security)

## System Information

Check system uptime:

```bash
uptime
```

Display CPU information:

```bash
lscpu
```

Check memory usage:

```bash
free -h
```

View disk space usage:

```bash
df -h
```

Check kernel version:

```bash
uname -r
```

## User Management

List all users:

```bash
cat /etc/passwd
```

Add a new user:

```bash
sudo useradd -m username
```

Change user password:

```bash
passwd username
```

Delete a user:

```bash
sudo userdel -r username
```

Check current user:

```bash
whoami
```

## Process Management

List running processes:

```bash
top
```

Find a process by name:

```bash
ps aux | grep process_name
```

Kill a process by PID:

```bash
kill -9 PID
```

View real-time system resource usage:

```bash
htop  # Requires installation: sudo apt install htop
```

## Disk Management

Check disk usage by directory:

```bash
du -sh *
```

List all mounted filesystems:

```bash
mount
```

Format a disk:

```bash
sudo mkfs.ext4 /dev/sdX
```

## File Management

List files in a directory:

```bash
ls -l
```

Copy a file:

```bash
cp source destination
```

Move a file:

```bash
mv source destination
```

Delete a file:

```bash
rm filename
```

Find a file:

```bash
find /path -name filename
```

## Permissions & Ownership

Change file permissions:

```bash
chmod 755 filename
```

Change file owner:

```bash
chown user:group filename
```

View file permissions:

```bash
ls -l filename
```

## Package Management

### Debian-based (Ubuntu, Debian)

Update package lists:

```bash
sudo apt update
```

Upgrade installed packages:

```bash
sudo apt upgrade
```

Install a package:

```bash
sudo apt install package_name
```

Remove a package:

```bash
sudo apt remove package_name
```

### RHEL-based (CentOS, Fedora)

Update packages:

```bash
sudo yum update
```

Install a package:

```bash
sudo yum install package_name
```

Remove a package:

```bash
sudo yum remove package_name
```

## System Performance & Monitoring

Monitor disk I/O usage:

```bash
iotop  # Requires installation: sudo apt install iotop
```

Monitor system performance with sar:

```bash
sar -u 5 10  # CPU usage every 5 sec, 10 times
```

Monitor memory usage:

```bash
vmstat 1 5  # Shows memory stats every second for 5 times
```

Monitor system resource usage interactively:

```bash
dstat -tcm  # Requires installation: sudo apt install dstat
```

## Logs & Debugging

View system logs:

```bash
sudo journalctl -xe
```

Check logs for a specific service:

```bash
sudo journalctl -u service_name
```

View kernel logs:

```bash
dmesg | tail -20
```

## Archiving & Compression

Create a tar archive:

```bash
tar -cvf archive.tar directory/
```

Extract a tar archive:

```bash
tar -xvf archive.tar
```

Compress a file with gzip:

```bash
gzip filename
```

Decompress a gzip file:

```bash
gunzip filename.gz
```

## Job Scheduling

Schedule a job with cron:

```bash
crontab -e
```

List scheduled cron jobs:

```bash
crontab -l
```

Schedule a one-time job with at:

```bash
echo "command" | at now + 10 minutes
```

## System Security

Check firewall status:

```bash
sudo ufw status
```

Enable firewall:

```bash
sudo ufw enable
```

Disable firewall:

```bash
sudo ufw disable
```

View failed SSH login attempts:

```bash
sudo grep "Failed password" /var/log/auth.log
```

Scan system for rootkits:

```bash
sudo rkhunter --check
```

Check open network connections:

```bash
sudo lsof -i
```

Monitor system logs for security threats:

```bash
dmesg | tail -20
```
