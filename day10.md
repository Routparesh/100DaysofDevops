## Day 10: Linux Bash Scripts

The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 3 in Stratos Datacenter, and they need to create a bash script named news_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 3).

a. Create a zip archive named xfusioncorp_news.zip of /var/www/html/news directory.

b. Save the archive in /backup/ on App Server 3. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on Nautilus Backup Server.

c. Copy the created archive to Nautilus Backup Server server in /backup/ location.

d. Please make sure script won't ask for password while copying the archive file.
Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.

Step 1 — Prepare the directories
Make sure /scripts and /backup exist:

```bash
sudo mkdir -p /scripts /backup
sudo chown banner:banner /scripts /backup
```

Step 2 — Set up passwordless SSH to Nautilus Backup Server
You need to figure out the backup server hostname/IP and the username (likely backup or clint for App Server 3 in Stratos tasks).
On App Server 3:

```bash
ssh-keygen -t rsa
```

(Press Enter through all prompts.)

Copy the public key to the Nautilus Backup Server:

```bash
ssh-copy-id <username>@<nautilus_backup_server_ip>
```

Test:

```bash
ssh <username>@<nautilus_backup_server_ip>
```

If it logs in without a password, you’re good.
Step 3 — Create the news_backup.sh script

```bash
nano /scripts/news_backup.sh
```

```bash
#!/bin/bash

# Variables
SRC_DIR="/var/www/html/news"
BACKUP_NAME="xfusioncorp_news.zip"
LOCAL_BACKUP_DIR="/backup"
REMOTE_USER="<username>"
REMOTE_HOST="<nautilus_backup_server_ip>"
REMOTE_BACKUP_DIR="/backup"

# Create local backup
zip -r "$LOCAL_BACKUP_DIR/$BACKUP_NAME" "$SRC_DIR"

# Copy backup to Nautilus Backup Server
scp "$LOCAL_BACKUP_DIR/$BACKUP_NAME" "${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_BACKUP_DIR}"
```

Replace <username> and <nautilus_backup_server_ip> with the real values.
Step 4 — Make the script executable

```bash
chmod +x /scripts/news_backup.sh

/scripts/news_backup.sh

```
