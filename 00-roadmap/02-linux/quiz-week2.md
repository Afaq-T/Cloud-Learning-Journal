# Week 2 – Linux Quiz (with Answers)

1. **What command shows you the full path of your current directory?**  
   `pwd` (Print Working Directory)

2. **How do you list all files in a directory, including hidden files, with detailed permissions?**  
   `ls -la`

3. **Which directory contains system configuration files?**  
   `/etc`

4. **Where are user home directories typically located?**  
   `/home`

5. **What command would you use to change your current directory to `/var/log`?**  
   `cd /var/log`

6. **How do you create a new empty file called `test.txt`?**  
   `touch test.txt`

7. **What command copies a file named `file1.txt` to `file2.txt`?**  
   `cp file1.txt file2.txt`

8. **How do you rename or move a file?**  
   `mv oldname newname`

9. **What command deletes a file named `old.log`?**  
   `rm old.log`

10. **What does the `cat` command do?**  
    Displays the contents of a file (concatenates files).

11. **How can you view the first 10 lines of a file?**  
    `head filename`

12. **What command shows you the last few lines of a file and updates in real time?**  
    `tail -f filename`

13. **What does the `chmod 755 script.sh` command do?**  
    Sets permissions: owner can read, write, execute (7); group can read and execute (5); others can read and execute (5).

14. **How do you check which user you are currently logged in as?**  
    `whoami`

15. **What command displays disk space usage in human‑readable format?**  
    `df -h`

16. **How do you see all running processes on the system?**  
    `ps aux`

17. **What command shows live system resource usage and lets you sort by CPU?**  
    `top` (press `P` to sort by CPU)

18. **How do you check which network ports are listening on your system?**  
    `ss -tuln` or `netstat -tuln`

19. **What command would you use to test internet connectivity by sending 4 packets to `8.8.8.8`?**  
    `ping -c 4 8.8.8.8`

20. **How do you view the logs for a specific service (e.g., `ssh`)?**  
    `journalctl -u ssh`