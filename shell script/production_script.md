
### 1. Backup Script
This script creates a backup of a specified directory.

```bash
#!/bin/bash

# Variables
SOURCE_DIR="/path/to/source"
BACKUP_DIR="/path/to/backup"
DATE=$(date +%Y%m%d%H%M%S)
BACKUP_NAME="backup-$DATE.tar.gz"

# Create backup
tar -czf $BACKUP_DIR/$BACKUP_NAME $SOURCE_DIR

# Log the backup
echo "Backup created: $BACKUP_NAME" >> /var/log/backup.log
```

### 2. User Account Management Script
This script adds a new user and sets up their home directory.

```bash
#!/bin/bash

# Variables
USERNAME=$1
PASSWORD=$2

# Check if user exists
if id "$USERNAME" &>/dev/null; then
    echo "User $USERNAME already exists."
    exit 1
fi

# Create user and set password
useradd -m $USERNAME
echo "$USERNAME:$PASSWORD" | chpasswd

# Set permissions
chmod 700 /home/$USERNAME

# Log the creation
echo "User $USERNAME created." >> /var/log/user_management.log
```

### 3. Disk Usage Monitoring Script
This script monitors disk usage and sends an alert if usage exceeds a threshold.

```bash
#!/bin/bash

# Variables
THRESHOLD=80
EMAIL="admin@example.com"

# Check disk usage
USAGE=$(df / | grep / | awk '{ print $5 }' | sed 's/%//g')

# Send alert if usage exceeds threshold
if [ $USAGE -gt $THRESHOLD ]; then
    echo "Disk usage is at $USAGE%" | mail -s "Disk Usage Alert" $EMAIL
fi
```

### 4. Service Monitoring Script
This script checks if a service is running and restarts it if it is not.

```bash
#!/bin/bash

# Variables
SERVICE="apache2"

# Check if service is running
if ! systemctl is-active --quiet $SERVICE; then
    # Restart service
    systemctl restart $SERVICE
    # Log the restart
    echo "$SERVICE was restarted." >> /var/log/service_monitor.log
fi
```

### 5. Log Rotation Script
This script rotates logs to prevent them from growing too large.

```bash
#!/bin/bash

# Variables
LOG_DIR="/var/log/myapp"
ARCHIVE_DIR="/var/log/myapp/archive"
DATE=$(date +%Y%m%d)

# Rotate logs
for LOG_FILE in $LOG_DIR/*.log; do
    mv $LOG_FILE $ARCHIVE_DIR/$(basename $LOG_FILE)-$DATE
    touch $LOG_FILE
done

# Compress old logs
find $ARCHIVE_DIR -type f -name "*.log-*" -exec gzip {} \;
```

6. Script that checks if Java is installed on a Linux system. If Java is not installed, the script will install it.

```bash
#!/bin/bash

# Function to check if Java is installed
check_java() {
    if java -version &>/dev/null; then
        echo "Java is already installed."
        return 0
    else
        echo "Java is not installed."
        return 1
    fi
}

# Function to install Java
install_java() {
    echo "Installing Java..."
    sudo apt update
    sudo apt install -y default-jdk
    if [ $? -eq 0 ]; then
        echo "Java installed successfully."
    else
        echo "Failed to install Java."
        exit 1
    fi
}

# Main script
if check_java; then
    echo "No action needed."
else
    install_java
fi
```



