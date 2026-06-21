# Linux Overview

## Definition
Linux is a family of open-source, Unix-like operating systems based on the Linux kernel. It is the dominant OS for enterprise servers, cloud infrastructure, and embedded systems.

## Why it exists
Windows is heavy, requires a GUI, and costs money to license. Linux is free, highly secure, incredibly performant, and can be managed entirely through text (CLI) remotely via SSH. It is the backbone of the internet and enterprise middleware like Edifecs.

## Commands
- `ls -la`: List all files/folders, showing hidden files and permission bits.
- `chmod 755 script.sh`: Change permissions (Owner=rwx, Group=rx, Others=rx).
- `chown user:group file`: Change file ownership.
- `grep -r "ERROR" /var/log/`: Recursively search for a string inside files.
- `awk -F'*' '{print $2}' file.txt`: Print the second column of a file separated by asterisks (excellent for X12).
- `tail -f server.log`: Watch a log file update in real-time.
- `du -sh * | sort -h`: Find out what is eating up disk space.
- `netstat -tulpn`: See which process is listening on which port.

## Architecture
- **Kernel**: The core. It talks directly to the CPU, memory, and hardware.
- **Shell**: The CLI interface (like `bash` or `zsh`) that takes human commands and translates them for the Kernel.
- **File System**: "Everything is a file" (even hardware devices and active processes are represented as files in `/dev` or `/proc`).
- **Daemons**: Background services (like `sshd` or `cron`) that run continuously.

## Interview Questions
**Q: "A production server is running out of disk space, and you suspect a log file is the culprit. How do you find and fix it?"**
*Answer*: I use `du -sh * | sort -h` to find the massive file. Crucially, I DO NOT use `rm` to delete it, because if the application is still writing to it, the OS won't free the disk space. Instead, I truncate it safely using `> server.log` or `cat /dev/null > server.log`.

**Q: "How do you find which application is blocking port 8080?"**
*Answer*: I run `netstat -tulpn | grep 8080` (or `lsof -i :8080`) to get the PID (Process ID), and then run `ps -ef | grep <PID>` to see exactly what application it is.

## Cheat Sheet
| Task | Command |
| :--- | :--- |
| Extract an archive | `tar -xvf archive.tar.gz` |
| Create an archive | `tar -cvf archive.tar folder/` |
| View active processes | `top` or `htop` |
| Safely kill a process | `kill -15 <PID>` (SIGTERM) |
| Force kill a process | `kill -9 <PID>` (SIGKILL - dangerous) |
| Find a file by name | `find / -name "server.xml"` |
