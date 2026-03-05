# Linux Cheatsheet

## Navigation Commands
- **ls**: `ls [options]` | `ls -la` | List files (-a=hidden, -l=detailed)
- **cd**: `cd [directory]` | `cd /var/log` | Change directory (`~`=home, `..`=parent)
- **pwd**: `pwd` | `pwd` | Show current working directory path
- **find**: `find [path] -name "pattern"` | `find /home -name "*.txt"` | Search files by name
- **which**: `which [command]` | `which ls` | Show full path to executable command

## File Commands
- **cat**: `cat [file]` | `cat /etc/hosts` | Display file content
- **head**: `head [-n lines] [file]` | `head -n 5 /var/log/syslog` | Show first lines
- **tail**: `tail [-n lines] [-f] [file]` | `tail -n 10 /var/log/auth.log` | Show last lines (live with -f)
- **cp**: `cp [options] source dest` | `cp file.txt /backup/` | Copy files/directories
- **mv**: `mv source dest` | `mv old.txt new.txt` | Move/rename files

## Permission Commands
- **chmod**: `chmod [mode] [file]` | `chmod 755 script.sh` | Change permissions (755=rwx,rx,rx)
- **chown**: `chown [user:group] [file]` | `chown user:group file.txt` | Change file ownership
- **ls -la**: `ls -la [path]` | `ls -la /etc` | List all files with permissions/ownership
- **id**: `id [user]` | `id` | Show user/group IDs
- **whoami**: `whoami` | `whoami` | Show current username

## System Commands
- **df**: `df -h` | `df -h` | Show disk space usage
- **free**: `free -h` | `free -h` | Show RAM/memory usage
- **uptime**: `uptime` | `uptime` | Show system uptime + load average
- **top**: `top` | `top` | Live process monitor (CPU, memory)
- **ps**: `ps aux` | `ps aux` | List all running processes

## Networking Commands
- **ss**: `ss -tuln` | `ss -tuln` | Show network connections/ports
- **curl**: `curl [URL]` | `curl https://example.com` | Download/test web content
- **dig**: `dig [domain]` | `dig google.com` | DNS lookup (get domain IPs)
- **ping**: `ping [host/IP]` | `ping 8.8.8.8` | Test network connectivity
- **ip addr**: `ip addr` | `ip addr` | Show network interfaces/IP addresses

## Log Commands
- **journalctl**: `journalctl -xe` | `journalctl -xe` | View systemd system logs
- **tail -f**: `tail -f [file]` | `tail -f /var/log/syslog` | Watch logs live
- **cat**: `cat [logfile]` | `cat /var/log/syslog` | Display complete log file
- **grep**: `grep "pattern" [file]` | `grep "error" /var/log/app.log` | Search text in logs
- **dmesg**: `dmesg | tail` | `dmesg | tail` | View kernel/hardware logs
