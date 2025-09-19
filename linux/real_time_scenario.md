# **Real-Time Scenario-Based Linux Implementations**

This document provides practical, real-world Linux command-line solutions for common system administration and troubleshooting tasks. Each scenario includes the command syntax, brief explanation, and important notes for safe and effective usage.

---

## 1. **Find and Kill the Process Consuming Maximum Memory**

**Command:**
```bash
ps aux --sort=-%mem | head -n 5
kill -9 [PID]
```

**Explanation:**
- `ps aux --sort=-%mem` lists all processes sorted by memory usage (descending).
- `head -n 5` displays the top 5 memory-consuming processes.
- `kill -9 [PID]` forcefully terminates the process with the specified Process ID.

> ⚠️ **Note:** If you receive the error `Operation not permitted`, prepend the command with `sudo`:  
> ```bash
> sudo kill -9 [PID]
> ```

---

## 2. **Find Files Modified in the Last 120 Minutes in a Directory**

**Command:**
```bash
find [folder_name]/ -type f -mmin -120
```

**Explanation:**
- `-type f` ensures only files (not directories) are listed.
- `-mmin -120` filters files modified within the last 120 minutes.

> ✅ Replace `[folder_name]` with the actual directory path (e.g., `/var/log/`).

---

## 3. **Create a Temporary User with an Expiration Date**

**Commands:**
```bash
sudo useradd -e 2025-06-01 [username]
sudo passwd [username]
sudo chage -d 0 [username]
```

**Explanation:**
- `useradd -e YYYY-MM-DD` creates a user account that expires on the specified date.
- `passwd` sets a password for the new user.
- `chage -d 0` forces the user to change their password on first login.

> 📅 Format: `YYYY-MM-DD`. Adjust the date and username as needed.

---

## 4. **Identify Which Process is Using a Specific Port**

**Command:**
```bash
sudo lsof -i :8080
```

**Explanation:**
- `lsof -i :[PORT]` lists all processes using the specified network port.
- Requires `sudo` for full visibility across all users.

> 🔄 Replace `8080` with any port number you wish to inspect (e.g., `:22`, `:80`, `:3306`).

---

## 5. **List or Remove Cron Jobs for a Specific User**

**Commands:**
```bash
crontab -u [username] -l    # List cron jobs
crontab -u [username] -r    # Remove all cron jobs
```

**Explanation:**
- `-l` lists the user’s scheduled cron jobs.
- `-r` removes all cron jobs for the specified user.

> ⚠️ Use `-r` with caution — this action is irreversible without backups.

---

## 7. **Find and Terminate Processes Consuming Maximum CPU**

**Commands:**
```bash
top -o %CPU                 # Interactive view, sorted by CPU usage
ps aux --sort=-%cpu | head -10   # Static list of top 10 CPU-consuming processes
kill [PID]                  # Gracefully terminate a process
```

**Explanation:**
- `top -o %CPU` opens an interactive process viewer sorted by CPU usage.
- `ps aux --sort=-%cpu | head -10` outputs the top 10 processes by CPU usage.
- `kill [PID]` sends a SIGTERM signal to gracefully stop the process. Use `kill -9 [PID]` only if unresponsive.

> 💡 Prefer `kill [PID]` over `kill -9` to allow processes to clean up before exiting.

---

## 8. **View System Logs Before and During VM Reboot**

**Commands:**
```bash
journalctl -b -1                            # Full logs from previous boot
journalctl -b -1 | grep -i "fail\|error\|crash"   # Filter for keywords
journalctl -b -1 -p err                     # Show only error-level messages
```

**Explanation:**
- `-b -1` refers to the boot session immediately before the current one.
- `grep -i` performs case-insensitive search for critical keywords.
- `-p err` filters logs by priority (error or higher).

> 📊 Useful for diagnosing crashes, failed services, or boot issues.

---

## 9. **Find Zombie Processes**

**Command:**
```bash
ps aux | awk '{ if ($8 == "Z") print $0; }'
```

**Explanation:**
- Lists all processes where the status (`$8`) is `"Z"` (Zombie).
- Zombie processes are dead processes still listed in the process table (waiting for parent to read exit status).

> 🧟 Zombies consume no resources but may indicate application bugs. Usually resolved by restarting the parent process.

---

## 10. **Check System Uptime**

**Command:**
```bash
uptime
```

**Explanation:**
- Displays how long the system has been running, current time, number of users, and load averages.

> 🕒 Output example:  
> `12:34:56 up 15 days, 3:22, 2 users, load average: 0.12, 0.09, 0.05`

---

## 11. **Find All Executable Files in a Directory**

**Command:**
```bash
find [folder_name]/ -type f -executable
```

**Explanation:**
- `-type f` ensures only files are considered.
- `-executable` filters files that are executable by the current user.

> 📁 Replace `[folder_name]` with your target directory (e.g., `/usr/bin/`).

---

## 15. **Perform DNS Lookup in Linux**

**Command:**
```bash
nslookup [domain_or_url]
```

**Example:**
```bash
nslookup google.com
```

**Explanation:**
- Queries DNS to resolve domain names to IP addresses.
- Shows authoritative name servers and associated records.

> 🌐 Alternative: `dig [domain]` for more detailed DNS diagnostics.

---

## 17. **Broadcast System Shutdown or Reboot with Message (Best Practice)**

**Commands:**
```bash
sudo shutdown -r +1 "Rebooting for maintenance. Save your work."
```

**Options:**
- `-r` → Reboot after shutdown (omit to power off).
- Time formats:
  - `now` → Immediate reboot
  - `+5` → Reboot in 5 minutes
  - `14:30` → Reboot at 2:30 PM

**To Cancel:**
```bash
sudo shutdown -c "Reboot cancelled. Maintenance postponed."
```

**Explanation:**
- Broadcasts a wall message to all logged-in users.
- Gives users time to save work before system restarts.

> 📢 Always notify users before rebooting production systems.

---

## 18. **Check Currently Logged-In Users**

**Command:**
```bash
w
```

**Explanation:**
- Shows who is logged in, their terminals, login times, idle time, and currently running processes.

> 👥 Alternative: `who` for simpler output, or `users` for just usernames.

---

## 19. **Kill All Processes Owned by a Specific User**

**Command:**
```bash
pkill -u [username]
```

**Explanation:**
- Terminates all processes associated with the specified user.
- Sends `SIGTERM` by default (graceful termination).

> ⚠️ Use with extreme caution — this will terminate ALL user sessions and processes.

---

## ✅ Best Practices & Notes

- Always test commands in non-production environments first.
- Prefer graceful termination (`kill [PID]`) over forceful (`kill -9 [PID]`).
- Use `sudo` judiciously — understand what each command does before elevating privileges.
- Document changes and notify users before system-wide actions (e.g., reboots).

---
