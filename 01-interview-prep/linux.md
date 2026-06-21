# Linux & CLI

## 1. Architecture & The Need
- **The Need**: Enterprise software like Edifecs does not run on Windows laptops; it runs on high-performance, secure, headless Linux servers.
- **Architecture**: A monolithic kernel interacting directly with hardware. No Graphical User Interface (GUI). Everything is a file, and everything is accessed via the Command Line Interface (CLI).

## 2. Core Concepts
- **File System Hierarchy**: `/var/log` (logs), `/etc` (configurations), `/home` (user profiles).
- **Permissions**: Read (4), Write (2), Execute (1). E.g., `chmod 777` gives everyone all permissions (dangerous).
- **Daemons**: Background services that keep the application running (like the Edifecs JVM).

## 3. Basic Daily Usage (Must-Know Commands)
- `ls -la`: List all files, including hidden files, with their permissions and sizes.
- `cd /path/to/dir`: Change directories.
- `cat file.txt`: Print the entire file to the screen (never use on massive files).
- `tail -f server.log`: Watch the end of a log file in real-time as the application writes to it.
- `grep "ERROR" server.log`: Search for the word "ERROR" in the log file.

## 4. Advanced Commands & Usage
- `du -sh * | sort -h`: Calculate folder sizes and sort them to find what is eating up disk space.
- `> file.log` or `cat /dev/null > file.log`: Safely truncate a file to 0 bytes without deleting the file descriptor (crucial for active application logs).
- `netstat -tulpn | grep 8080`: Find exactly which process is actively listening on port 8080.
- `awk -F'*' '{print $14}'`: Use AWK to parse an X12 string separated by `*` and print only the 14th element.

---

## Interview Question Deep Dive

### Q: "A production server is running out of disk space, and you suspect a log file is the culprit. How do you find and fix it via CLI?"

**30-Second Answer**: I would use `df -h` to verify which mount is full, then run `du -sh * | sort -h` to locate the massive log file. To fix it without crashing the application, I would truncate the file using `> server.log` rather than deleting it.

**2-Minute Answer**: First, type `df -h` to ensure the `/var/log` or application partition is actually at 100%. Then, navigate to the application directory and run `du -sh * | sort -hr | head -n 10` to find the 10 largest files. Usually, it's an Edifecs `server.log` or a massive `.dat` payload file left in a temp folder. 

Crucially, **you cannot just use `rm server.log`**. If the Java JVM is still running and actively writing to that file, it holds the file descriptor open. The `rm` command deletes the pointer, but the OS won't free the disk space until the JVM stops. Instead, I use `> server.log` to truncate the file to 0 bytes while allowing the application to keep writing.

**Deep Dive Answer**: Once the immediate fire is out, the root cause must be addressed. I would check the Edifecs log4j configurations to ensure logging is set to `WARN` or `ERROR` in production, not `DEBUG` or `TRACE`. Then, I would ensure `logrotate` is configured correctly at the OS level to compress and cycle logs daily.

**Real Example**: When debugging a failure in the Humana project, I didn't pull the 5GB log locally; I used `grep -a "ISA\*.*123456789" server.log | awk -F'*' '{print $14}'` to instantly extract the exact X12 segment I needed directly on the Linux server.

**Follow-up Questions**:
- *Interviewer*: "How do you view a log file in real-time as data is written?" (Answer: `tail -f server.log`).
