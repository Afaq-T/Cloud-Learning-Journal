
# Week 2: Linux Basics – My Notes

**Source:** NetworkChuck's "Linux for Hackers" series (Episodes 1-4)

## Why Linux?
- **Linux is Everywhere:** It's the foundation for most websites, servers, and cloud platforms (like Azure). If you want to work in IT, cloud, or cybersecurity, you will use Linux.
- **It's Open Source:** The code is free and open for anyone to look at, change, and improve. This makes it very flexible and secure.
- **It's Fast and Secure:** Linux is efficient and less prone to viruses than other operating systems, which is why it's the top choice for hackers and for running servers.
- **The Terminal is Your Power Tool:** Unlike Windows or Mac, where you mostly click on things (GUI), in Linux you type commands (CLI). It's faster and more powerful once you get the hang of it.

## Your First Commands: Navigating the Filesystem
Think of the Linux filesystem like a tree. The very top is the root, represented by a forward slash (`/`). Everything else is a branch (folder) coming off of it.

- **`pwd` (Print Working Directory):** Tells you exactly where you are in the filesystem tree. It prints your current location.
  ```bash
  pwd

  *Example output:* `/home/your-username`

- **`ls` (List):** Shows what's inside your current folder – all files and subfolders.
  ```bash
  ls
  ```
  *Try `ls -la` for a more detailed list, including hidden files (files that start with a dot).*

- **`cd` (Change Directory):** Moves you around the filesystem.
  ```bash
  cd Desktop    # Moves you into the 'Desktop' folder
  cd ..         # Moves you *up* one level, back to the parent folder
  cd /var/log   # Moves you directly to the '/var/log' folder from anywhere
  cd ~          # Takes you back to your home folder (/home/your-username)
  cd /          # Takes you all the way to the very top, the root directory
  ```

## The Linux Filesystem Explained
A key concept in Linux is that **"everything is a file"** – your documents, your commands, even your hardware. The system is organized with specific folders for specific purposes:

- **`/` (The Root):** The top-level directory. Every single file and folder on your system is inside `/`.

- **`/bin` and `/sbin`:** These folders hold the essential command binaries (programs) that the system needs to run. `/bin` has commands for all users (`ls`, `pwd`, `cp`), while `/sbin` has commands for system administration (usually requires `sudo`).

- **`/etc`:** This is where all the **configuration files** for your system and applications live. Think of it as the "settings" folder for your whole computer.
  ```bash
  ls /etc    # See all the config files
  ```

- **`/home`:** This is where regular users store their personal files and settings. Each user gets their own folder inside `/home` (e.g., `/home/student`, `/home/thor`).

- **`/var`:** This folder contains data that **changes (varies)** over time, most importantly, **log files**. System logs are usually in `/var/log`.
  ```bash
  ls /var/log    # See all the log files
  ```

- **`/tmp`:** A place for **temporary files**. Files here are often deleted when you restart the computer. Anyone can read and write here, so it's useful for testing but not for storing important things.

- **`/dev`:** This folder holds files that represent your **devices**, like your hard drive, keyboard, or monitor. This is the "everything is a file" concept in action.

## Understanding Files as Data (Not Just Programs)
- **`cat` (Concatenate):** The `cat` command is a quick way to look inside a text file and print its contents to the terminal.
  ```bash
  cat /etc/passwd    # Shows you the list of users on the system
  ```
  Because everything is a file, you can even use `cat` to look at the files that *are* commands, but it will just show you a bunch of unreadable machine code.

- **`which`:** This command tells you the exact location of another command's file. It's like asking, "Where is this program actually stored?"
  ```bash
  which ls           # Output might be /usr/bin/ls
  which cat
  ```

## Users, Groups, and the Power of `sudo`
Linux is a multi-user system, so it has strict rules about who can do what.

- **`root` (The Superuser):** This is the all-powerful administrator account. It can do absolutely anything. Because it's so powerful, you don't log in as `root` for everyday tasks – it's too dangerous. One wrong command could break the whole system.

- **`sudo` (Superuser Do):** This is the magic word. If a regular user needs to do an administrative task (like installing software or editing a system config file), they put `sudo` in front of the command.
  ```bash
  sudo apt update    # Updates the list of available software (needs admin power)
  ```
  The system will ask for **your** password to make sure it's really you. This is much safer than being the `root` user all the time.

- **Adding Users:** You can create new users with the `adduser` command. You'll need `sudo` to do this.
  ```bash
  sudo adduser thor   # Creates a new user named 'thor'
  ```

- **The `sudo` Group:** Not every user is allowed to use `sudo`. You have to be a member of the special **`sudo` group**. Think of it as the "VIP club" for users with administrative privileges.

- **`whoami`:** A simple command to remind you of the username you are currently logged in as.
  ```bash
  whoami
  ```

## File Permissions (Brief Overview)
Every file and folder has an **owner** and belongs to a **group**. Permissions are set for three types of people:
1. **Owner (u):** The user who owns the file.
2. **Group (g):** Other users who are part of the file's group.
3. **Others (o):** Everyone else on the system.

For each of these, you can set three types of permissions:
- **Read (r):** Look at the file's contents, or list the files in a folder.
- **Write (w):** Change or delete the file, or add/remove files in a folder.
- **Execute (x):** Run the file as a program, or `cd` into a folder.

When you run `ls -l`, you'll see something like `-rwxr-xr--`. This is a code that shows the permissions.
- The first character (`-`) tells you it's a file (a `d` would mean it's a directory).
- The next three (`rwx`) are the **owner's** permissions (read, write, execute).
- The next three (`r-x`) are the **group's** permissions (read and execute, but not write).
- The last three (`r--`) are **others'** permissions (read only).

## Processes
- **What is a Process?** Any program that is running on your computer is a **process**. Every command you run, every background service, everything.
- **`ps aux`:** This is the command to see all the processes currently running on the system. It shows you a list with important info like:
  - **USER:** Who is running the process.
  - **PID (Process ID):** A unique identification number for that process. Think of it as the process's ID card number.
  - **%CPU / %MEM:** How much of your computer's power it's using.
  - **COMMAND:** The name of the program.
- **`kill [PID]`:** If a program freezes or you just need to stop it, you can use the `kill` command followed by its PID.
  ```bash
  # First, find the PID of the program you want to stop (e.g., with 'ps aux | grep firefox')
  # Then, kill it
  kill 1234    # Replace 1234 with the actual PID
  ```
  This sends a polite "please stop" signal. If it doesn't respond, you can use `kill -9 [PID]` to force it to stop immediately.

## A Cool Trick: The `history` Command
You can see a list of every command you've typed recently by using:
```bash
history
```
This is great for remembering a complicated command you used earlier.
```
