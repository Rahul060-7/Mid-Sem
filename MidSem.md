# Daily System Logger Script (Updated Version)

### **Name:** Paras Bhall  
### **SAP ID:** 590029319  
### **Date:** 2025-11-09

---

## **AIM**
To create and schedule a shell script that:
- Logs system information daily
- Stores logs in a dedicated folder
- Rotates logs older than 7 days
- Runs automatically using **cron**

---

## **Requirements**
- Any Linux distribution (e.g., Linux Mint / Ubuntu / Pop!_OS)
- Text editor (Nano, Vim, VS Code, etc.)
- Cron service enabled

---

## **Theory**
System administrators often automate logs to track performance and system health. This experiment focuses on:
1. Collecting system data: processes, memory, disk usage, user info
2. Saving daily logs with date-based filenames
3. Deleting old logs automatically
4. Scheduling tasks using `cron`

---

## **Exercise 1: Creating the Daily Log Script**

### **Task:**
Create a Bash script that saves system info and rotates logs older than 7 days.

### **Script (daily_log.sh):**
```bash
#!/bin/bash

LOG_DIR="$HOME/daily_logs"
mkdir -p "$LOG_DIR"

# Create a log file with today's date
LOG_FILE="$LOG_DIR/log_$(date +"%Y-%m-%d").txt"

# Record system information
{
    echo "====== Daily System Log ======"
    echo "Date: $(date)"
    echo "User: $USER"
    echo

    echo "====== Top 5 Running Processes (by CPU) ======"
    ps -eo pid,user,comm,%cpu,%mem --sort=-%cpu | head -n 6
    echo

    echo "====== Disk Usage ======"
    df -h
    echo

    echo "====== Memory Usage ======"
    free -h
} > "$LOG_FILE"

# Delete logs older than 7 days
find "$LOG_DIR" -type f -name "log_*.txt" -mtime +7 -exec rm {} \;

echo "Log saved to: $LOG_FILE"
```

### **Output Screenshot:**
<p align="center">
<img src="input.png" width="900">
</p>

---

## **Exercise 2: Scheduling the Script Using Cron**

### **Task:**
Schedule the script to run daily.

### **Steps:**
1. Open crontab:
```bash
crontab -e
```

2. Add this line:
```bash
0 20 * * * /home/parasjaat34/daily_log.sh
```

This runs the script.

### **Cron Format Reminder:**
```
m h dom mon dow command
```

### **Cron Screenshot:**
<p align="center">
<img src="cron.png" width="900">
</p>
---

## **Final Output**
The script successfully:
- Creates a new log file daily
- Shows running processes, memory usage, disk usage
- Deletes old logs (older than 7 days)
- Runs automatically via cron

---
<p align="center">
<img src="out1.png" width="900">
</p>

## **Conclusion**
This experiment demonstrates automation using shell scripting and cron. The daily log script efficiently captures system information and maintains a clean log directory by removing older log files. Cron ensures the script runs consistently without manual intervention.

