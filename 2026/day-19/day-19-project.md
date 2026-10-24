# Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab


### Task 1: Log Rotation Script
Create `log_rotate.sh` that:
1. Takes a log directory as an argument (e.g., `/var/log/myapp`)
2. Compresses `.log` files older than 7 days using `gzip`
3. Deletes `.gz` files older than 30 days
4. Prints how many files were compressed and deleted
5. Exits with an error if the directory doesn't exist

#!/bin/bash

# Exit on error, unset variables, and pipe failures
set -euo pipefail

# 1. Check if an argument was provided
if [ -z "${1:-}" ]; then
    echo "Error: No log directory provided."
    echo "Usage: $0 /path/to/log/dir"
    exit 1
fi

LOG_DIR="$1"

# 5. Exit with an error if the directory doesn't exist
if [ ! -d "$LOG_DIR" ]; then
    echo "Error: Directory '$LOG_DIR' does not exist."
    exit 1
fi

compressed_count=0
deleted_count=0

echo "----------------------------------------"
echo "Starting log rotation for: $LOG_DIR"
echo "----------------------------------------"

# 2. Compress .log files older than 7 days using gzip
while IFS= read -r -d '' file; do
    gzip "$file"
    compressed_count=$((compressed_count + 1))
    echo "[COMPRESSED] $file"
done < <(find "$LOG_DIR" -name "*.log" -type f -mtime +7 -print0 2>/dev/null)

# 3. Delete .gz files older than 30 days
while IFS= read -r -d '' file; do
    rm -f "$file"
    deleted_count=$((deleted_count + 1))
    echo "[DELETED]    $file"
done < <(find "$LOG_DIR" -name "*.gz" -type f -mtime +30 -print0 2>/dev/null)

# 4. Print how many files were compressed and deleted
echo "----------------------------------------"
echo "Log Rotation Summary:"
echo "  - Files compressed (.log > 7 days): $compressed_count"
echo "  - Files deleted (.gz > 30 days):    $deleted_count"
echo "----------------------------------------"
echo "Log rotation completed successfully."




-------------

<img width="756" height="278" alt="image" src="https://github.com/user-attachments/assets/2275465a-f7a7-45d1-9666-96bd970e8050" />

---

### Task 2: Server Backup Script
Create `backup.sh` that:
1. Takes a source directory and backup destination as arguments
2. Creates a timestamped `.tar.gz` archive (e.g., `backup-2026-02-08.tar.gz`)
3. Verifies the archive was created successfully
4. Prints archive name and size
5. Deletes backups older than 14 days from the destination
6. Handles errors — exit if source doesn't exist


#!/bin/bash

# Exit on error, unset variables, and pipe failures
set -euo pipefail

# 1. Check if both arguments are provided
if [ $# -lt 2 ]; then
    echo "Error: Missing arguments."
    echo "Usage: $0 <source_directory> <destination_directory>"
    exit 1
fi

SRC_DIR="$1"
DEST_DIR="$2"

# 6. Handle errors — exit if source doesn't exist
if [ ! -d "$SRC_DIR" ]; then
    echo "Error: Source directory '$SRC_DIR' does not exist."
    exit 1
fi

# Ensure destination directory exists (creates it if missing)
mkdir -p "$DEST_DIR"

# 2. Create a timestamped .tar.gz archive
TIMESTAMP=$(date +%Y-%m-%d)
ARCHIVE_NAME="backup-${TIMESTAMP}.tar.gz"
ARCHIVE_PATH="$DEST_DIR/$ARCHIVE_NAME"

echo "----------------------------------------"
echo "Starting backup of: $SRC_DIR"
echo "----------------------------------------"

# Create the compressed tarball (-C handles clean relative archiving)
tar -czf "$ARCHIVE_PATH" -C "$(dirname "$SRC_DIR")" "$(basename "$SRC_DIR")"

# 3. Verify the archive was created successfully
if [ -f "$ARCHIVE_PATH" ]; then
    echo "[SUCCESS] Archive created."
else
    echo "[ERROR] Failed to create archive."
    exit 1
fi

# 4. Print archive name and size
ARCHIVE_SIZE=$(du -h "$ARCHIVE_PATH" | cut -f1)
echo "----------------------------------------"
echo "Backup Summary:"
echo "  - File Name: $ARCHIVE_NAME"
echo "  - Location:  $ARCHIVE_PATH"
echo "  - Size:      $ARCHIVE_SIZE"
echo "----------------------------------------"

# 5. Delete backups older than 14 days from the destination
echo "Checking for old backups (> 14 days)..."
find "$DEST_DIR" -name "backup-*.tar.gz" -type f -mtime +14 -exec rm -f {} \;
echo "Backup and cleanup process finished successfully."

---

### Task 3: Crontab
1. Read: `crontab -l` — This lists any cron jobs already running under your current user account
2. 
3. Understand cron syntax:
   ```
   * * * * *  command
   │ │ │ │ │
   │ │ │ │ └── Day of week (0-7)
   │ │ │ └──── Month (1-12)
   │ │ └────── Day of month (1-31)
   │ └──────── Hour (0-23)
   └────────── Minute (0-59)
   ```


4. <img width="624" height="237" alt="image" src="https://github.com/user-attachments/assets/e099ea25-416c-41cf-8e83-31dd1a459a48" />

   - Run `log_rotate.sh` every day at 2 AM

     0 2 * * * /home/ubuntu/log_rotate.sh /var/log/myapp
     
   - Run `backup.sh` every Sunday at 3 AM
  
   - 0 3 * * 0 /home/ubuntu/backup.sh /home/ubuntu/data /home/ubuntu/backups
  
   - 
   - Run a health check script every 5 minutes
  
   - */5 * * * * /home/ec2-user/system_info.sh >/dev/null 2>&1
  
   - 

---

### Task 4: Combine — Scheduled Maintenance Script
Create `maintenance.sh` that:
1. Calls your log rotation function
2. Calls your backup function
3. Logs all output to `/var/log/maintenance.log` with timestamps
4. Write the cron entry to run it daily at 1 AM

#!/bin/bash

# Exit on error, unset variables, and pipe failures
set -euo pipefail

# Define log file location
LOG_FILE="/var/log/maintenance.log"

# Function to print messages with timestamps
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1"
}

# Redirect all standard output and standard errors from this block into the log file
{
    log "=== Starting Scheduled Maintenance ==="

    # 1. Call your log rotation script/function
    log "Running log rotation..."
    if [ -f /home/ubuntu/log_rotate.sh ]; then
        /home/ubuntu/log_rotate.sh /var/log/myapp || log "[WARNING] Log rotation encountered an issue."
    else
        log "[ERROR] /home/ubuntu/log_rotate.sh not found."
    fi

    # 2. Call your backup script/function
    log "Running system backup..."
    if [ -f /home/ubuntu/backup.sh ]; then
        /home/ubuntu/backup.sh /home/ubuntu/data /home/ubuntu/backups || log "[WARNING] Backup encountered an issue."
    else
        log "[ERROR] /home/ubuntu/backup.sh not found."
    fi

    log "=== Maintenance Completed Successfully ==="
    log "" # Blank line for spacing between runs

} >> "$LOG_FILE" 2>&1
---


