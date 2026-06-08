# Day 07 - Linux File System Hierarchy & Scenario-Based Practice

## Part 1: Linux File System Hierarchy

### 1. / (Root Directory)

**Purpose:**
The root directory is the top-level directory in Linux. Every file and directory starts from here.

**Example Contents:**

```bash
ls -l /
```

Common directories:

* bin
* etc

**I would use this when:**
I need to navigate the Linux file system or locate major system directories.

---

### 2. /home

**Purpose:**
Contains home directories of normal users.

**Example Contents:**

```bash
ls -l /home
```

Common directories:

* shiv
* testuser

**I would use this when:**
Managing user files, scripts, and personal configurations.

---

### 3. /root

**Purpose:**
Home directory of the root user.

**Example Contents:**

```bash
ls -l /root
```

Common files:

* .bashrc
* .profile

**I would use this when:**
Performing administrative tasks as the root user.

---

### 4. /etc

**Purpose:**
Stores system-wide configuration files.

**Example Contents:**

```bash
ls -l /etc
```

Common files:

* hosts
* hostname

**I would use this when:**
Troubleshooting application or system configuration issues.

---

### 5. /var/log

**Purpose:**
Contains application and system log files.

**Example Contents:**

```bash
ls -l /var/log
```

Common files:

* syslog
* auth.log

**I would use this when:**
Investigating service failures, application errors, or system issues.

---

### 6. /tmp

**Purpose:**
Stores temporary files created by applications and users.

**Example Contents:**

```bash
ls -l /tmp
```

Common files:

* temp files
* application caches

**I would use this when:**
Checking temporary data or troubleshooting disk space issues.

---

### 7. /bin

**Purpose:**
Contains essential Linux command binaries required for system operation.

**Example Contents:**

```bash
ls -l /bin
```

Common commands:

* ls
* cp

**I would use this when:**
Finding critical system commands.

---

### 8. /usr/bin

**Purpose:**
Contains user-level command binaries and installed software.

**Example Contents:**

```bash
ls -l /usr/bin
```

Common commands:

* git
* python3

**I would use this when:**
Checking installed software executables.

---

### 9. /opt

**Purpose:**
Stores optional and third-party software packages.

**Example Contents:**

```bash
ls -l /opt
```

Common directories:

* application installations
* custom software

**I would use this when:**
Managing vendor applications and custom installations.

---

## Hands-on Commands

### Find Largest Log Files

```bash
du -sh /var/log/* 2>/dev/null | sort -h | tail -5
```

### View Hostname Configuration

```bash
cat /etc/hostname
```

### Check Home Directory

```bash
ls -la ~
```

---

# Part 2: Scenario-Based Practice

## Scenario 1: Service Not Starting

### Step 1

```bash
systemctl status myapp
```

**Why:**
Check whether the service is running, stopped, or failed.

### Step 2

```bash
journalctl -u myapp -n 50
```

**Why:**
Review recent logs for startup errors.

### Step 3

```bash
systemctl is-enabled myapp
```

**Why:**
Verify whether the service is configured to start after reboot.

### Step 4

```bash
journalctl -xe
```

**Why:**
Check system-wide error messages that may affect the service.

### What I Learned

Always start with service status, then inspect logs before making changes.

---

## Scenario 2: High CPU Usage

### Step 1

```bash
top
```

**Why:**
View live CPU and memory utilization.

### Step 2

```bash
ps aux --sort=-%cpu | head -10
```

**Why:**
Identify the processes consuming the most CPU.

### Step 3

```bash
pgrep -fl <process_name>
```

**Why:**
Verify process details.

### Step 4

```bash
top -p <PID>
```

**Why:**
Monitor a specific process in real time.

### What I Learned

Find the highest CPU consumer first before restarting or killing processes.

---

## Scenario 3: Finding Docker Service Logs

### Step 1

```bash
systemctl status docker
```

**Why:**
Check service health and recent logs.

### Step 2

```bash
journalctl -u docker -n 50
```

**Why:**
View the latest Docker service logs.

### Step 3

```bash
journalctl -u docker -f
```

**Why:**
Follow logs in real time.

### Step 4

```bash
docker logs <container_id>
```

**Why:**
Inspect logs for a specific container.

### What I Learned

Systemd-managed services store logs in journald and can be viewed using journalctl.

---

## Scenario 4: File Permission Issue

### Step 1

```bash
ls -l /home/user/backup.sh
```

**Why:**
Check current file permissions.

### Step 2

```bash
chmod +x /home/user/backup.sh
```

**Why:**
Add execute permission.

### Step 3

```bash
ls -l /home/user/backup.sh
```

**Why:**
Verify execute permission was applied.

### Step 4

```bash
./backup.sh
```

**Why:**
Run the script and confirm it works.

### What I Learned

A script requires execute permission (x) before it can run directly.

---

# Key Takeaways

* Linux logs are primarily located in `/var/log`.
* Configuration files are usually stored in `/etc`.
* User data is stored under `/home`.
* Troubleshooting should follow a structured process:

  * Check status
  * Review logs
  * Verify configuration
  * Apply fixes
  * Validate results

These concepts are essential for DevOps engineers handling production incidents, deployments, and system troubleshooting.
