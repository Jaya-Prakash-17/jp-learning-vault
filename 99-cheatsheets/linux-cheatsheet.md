# Linux & CLI Cheat Sheet

### Daily Commands (Must Know)
| Command | Action |
| :--- | :--- |
| `ls -la` | List all files/folders with hidden files and permissions. |
| `cd /dir` | Change directory. |
| `tail -f file.log` | Watch live updates at the end of a file. |
| `grep -r "ID" .` | Search recursively for a string inside all files in current dir. |
| `chmod 755 file` | Change permissions (Owner=rwx, Grp=rx, Other=rx). |
| `chown u:g file` | Change file owner and group. |

### Advanced Troubleshooting
| Command | Action |
| :--- | :--- |
| `du -sh * \| sort -h` | Find what is eating disk space (sorts folders by human-readable size). |
| `> file.log` | Safely truncate an active log file to 0 bytes without deleting it. |
| `netstat -tulpn` | Show all listening ports and the PIDs holding them. |
| `lsof -i :8080` | Find exactly what process is listening on port 8080. |
| `ps -ef \| grep java` | List all running Java processes. |
| `kill -15 <PID>` | Gracefully kill a process. |
| `kill -9 <PID>` | Force kill a process (Dangerous). |
| `awk -F'*' '{print $2}'` | Extract the 2nd column of an asterisk-delimited file (X12 extraction). |

### Key Concepts
- **Everything is a file**: Hardware, sockets, running processes (`/proc`).
- **File Descriptors**: Pointers. If Java is writing to `server.log`, deleting it (`rm`) removes the name, but the OS keeps the disk space occupied until Java stops. Always truncate (`>`).

### Interview Triggers
- 🚨 **"Server out of disk space"** ➡️ Trigger: `du -sh * | sort -h`. Fix with `> log.log`. Check `logrotate`.
- 🚨 **"Port already in use"** ➡️ Trigger: `netstat -tulpn | grep <port>`. Kill the rogue PID.
