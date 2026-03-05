# Linux Troubleshooting Scenarios

## Scenario: "A service is down"

**Goal:** Determine why a service isn't running and bring it back up.

**Steps:**
1. **Check service status**  
   `systemctl status <service-name>`  
   Replace `<service-name>` with the actual service (e.g., `nginx`, `ssh`, `docker`).  
   Look for the line that says `Active:` – it will show if the service is running, stopped, or failed.

2. **Examine the service logs**  
   `journalctl -u <service-name>`  
   This shows recent log messages from that service. Look for error messages that explain why it failed.

3. **Try restarting the service**  
   `sudo systemctl restart <service-name>`  
   If it starts successfully, the issue might have been temporary.

4. **If it fails again, check the configuration files**  
   Service configuration files are usually in `/etc/` (e.g., `/etc/nginx/nginx.conf`).  
   Look for syntax errors or misconfigurations. Many services have a built-in config test, e.g.:  
   `nginx -t`  (tests nginx configuration)

5. **Check if the service is enabled to start on boot**  
   `systemctl is-enabled <service-name>`  
   If you want it to start automatically, enable it:  
   `sudo systemctl enable <service-name>`

---

## Scenario: "A port is not listening"

**Goal:** Verify if a specific network port is open and listening for connections.

**Steps:**
1. **List all listening ports**  
   `ss -tuln`  
   This shows TCP (`-t`) and UDP (`-u`) listening sockets, with numeric addresses (`-n`).

2. **Search for the specific port**  
   `ss -tuln | grep :<port-number>`  
   Replace `<port-number>` with the port you care about (e.g., `:80`, `:22`).

3. **Interpret the result**  
   - If the port **appears** → the service is listening correctly.  
   - If it **does not appear** → the expected service is not running, or it’s listening on a different port.

4. **Check if the service is running**  
   `systemctl status <service-name>`  
   If the service is supposed to listen on that port but isn’t running, start it.

5. **Check the service’s configuration**  
   Look in its config file (often in `/etc/`) to see which port it’s configured to use.  
   For example, for an Apache web server, check `/etc/apache2/ports.conf`.

---

## Scenario: "Disk is full"

**Goal:** Identify which partition is full and clean up space.

**Steps:**
1. **Check overall disk usage**  
   `df -h`  
   Look for filesystems that are at 100% or very high usage. The `-h` flag makes the output human-readable (e.g., GB, MB).

2. **Find the largest directories**  
   `du -sh /* 2>/dev/null | sort -h`  
   This shows size of top‑level directories. You can drill down, e.g., `du -sh /var/* | sort -h`.

3. **Check common space hogs**  
   - **Log files:** `/var/log/` – especially large `.log` files.  
   - **Temporary files:** `/tmp/` – can be cleared safely after a reboot.  
   - **Caches:** `/var/cache/` – e.g., apt cache (`sudo apt clean`).

4. **Clean up logs (if safe)**  
   `sudo journalctl --vacuum-size=200M` (limits journal logs to 200 MB)  
   `sudo rm -rf /var/log/*.old` (delete old rotated logs – check first!)

5. **Remove unused packages**  
   `sudo apt autoremove`  
   `sudo apt autoclean`

6. **If the problem persists, consider adding more disk space** (cloud VMs can often resize volumes).

---

## Scenario: "Permission denied error"

**Goal:** Understand why you can’t access a file or directory and fix it.

**Steps:**
1. **Check current permissions**  
   `ls -la <file-or-directory>`  
   This shows the file’s owner, group, and permissions (e.g., `-rw-r--r--`).

2. **Identify the user and groups you belong to**  
   `whoami` – your username.  
   `groups` – list of groups you are a member of.

3. **Interpret the permissions**  
   The permission string is divided into three parts: owner, group, others.  
   Example: `-rwxr-x---` means owner can read/write/execute, group can read/execute, others have no access.  
   If you are not the owner and not in the group, you fall into “others” and may be denied.

4. **Temporary fix: use `sudo`**  
   If you have administrative rights, run the command with `sudo` to execute as root.

5. **Permanent fix: change ownership or permissions**  
   - Change owner: `sudo chown <new-owner> <file>`  
   - Change group: `sudo chgrp <new-group> <file>`  
   - Change permissions: `chmod 755 <file>` (e.g., owner full, group/others read+execute).  
   Use `chmod` with care – never set files to `777` unless absolutely necessary.

6. **Check parent directory permissions**  
   Sometimes you can’t access a file because you don’t have execute (`x`) permission on one of its parent directories.  
   Use `ls -ld /path/to/parent` to check.

---

## Scenario: "Cannot install packages"

**Goal:** Fix issues when `apt` fails to install or update software.

**Steps:**
1. **Update the package list**  
   `sudo apt update`  
   If this fails, check the error message.

2. **Check internet connectivity**  
   `ping 8.8.8.8` – if it fails, your network is down.  
   `ping google.com` – if the IP works but domain doesn’t, DNS is broken.

3. **Verify repository configuration**  
   `cat /etc/apt/sources.list`  
   Also check files in `/etc/apt/sources.list.d/`. Ensure the URLs are correct (e.g., `archive.ubuntu.com` for Ubuntu).

4. **Fix GPG key errors**  
   If you see “NO_PUBKEY” errors, add the missing key:  
   `sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys <KEY-ID>`  
   (Note: `apt-key` is deprecated; on newer systems use `sudo gpg --...` methods, but for quick fixes this still works.)

5. **Try installing with `--fix-missing`**  
   `sudo apt install --fix-missing <package>`

6. **Clean up and retry**  
   `sudo apt clean` (clears downloaded package files)  
   `sudo apt update --fix-missing`

7. **If all else fails, check if the package name is correct**  
   `apt search <keyword>` to find the exact package name.

---

## Scenario: "High CPU usage"

**Goal:** Find the process consuming too much CPU and take action.

**Steps:**
1. **Use `top` for live monitoring**  
   `top`  
   Press `P` to sort by CPU usage (highest first). Note the PID of the top process. Press `q` to quit.

2. **Use `ps` to get a static sorted list**  
   `ps aux --sort=-%cpu | head -20`  
   Shows top 20 CPU-consuming processes.

3. **Identify the process**  
   Look at the command name and user. Is it a known service (e.g., `apache2`, `mysql`)? Or an unknown/rogue process?

4. **Check further details**  
   `systemctl status <service-name>` (if it’s a service)  
   `lsof -p <PID>` (lists files opened by the process) – useful for investigation.

5. **Take action**  
   - If it’s a legitimate service that’s misbehaving, try restarting it:  
     `sudo systemctl restart <service-name>`  
   - If it’s a temporary process, you can kill it:  
     `kill <PID>` (graceful) or `kill -9 <PID>` (force).  
   - If it’s malware, investigate further and consider quarantining.

6. **Monitor after action**  
   Re-run `top` to ensure CPU usage returns to normal.
