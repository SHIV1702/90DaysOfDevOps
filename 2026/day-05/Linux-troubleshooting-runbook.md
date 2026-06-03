# Linux Troubleshooting Runbook

## Target Service / Process

Service: Docker

Purpose: Verify Docker daemon health and collect system resource information before taking corrective action.

---

# Environment Basics

## 1. Check Kernel Information

shiv@SHIV:~$ uname -a

Linux SHIV 5.15.167.4-microsoft-standard-WSL2 #1 SMP Tue Nov 5 00:21:55 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux

Observation:

* Ubuntu Linux kernel is running normally.
* No immediate OS-level issues detected.

## 2. Check OS Version

shiv@SHIV:~$ cat /etc/os-release

PRETTY_NAME="Ubuntu 24.04.4 LTS"

NAME="Ubuntu"

VERSION_ID="24.04"

VERSION="24.04.4 LTS (Noble Numbat)"

VERSION_CODENAME=noble

ID=ubuntu

ID_LIKE=debian

HOME_URL="https://www.ubuntu.com/"

SUPPORT_URL="https://help.ubuntu.com/"

BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"

PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"

UBUNTU_CODENAME=noble

LOGO=ubuntu-logo

Observation:

* Ubuntu 24.04 LTS confirmed.

---

# Filesystem Sanity

## 3. Create Test Directory

shiv@SHIV:~$ mkdir -p /tmp/runbook-demo

shiv@SHIV:~$ cd /tmp/runbook-demo/

shiv@SHIV:/tmp/runbook-demo$ l

total 0

Observation:

* Directory created successfully.

## 4. Copy and Verify File

shiv@SHIV:/tmp/runbook-demo$ cp /etc/hosts /tmp/runbook-demo/hosts-copy

shiv@SHIV:/tmp/runbook-demo$ ls -l /tmp/runbook-demo

total 4

-rw-r--r-- 1 shiv devops 394 Jun  3 05:13 hosts-copy

Observation:

* File copied successfully.
* Filesystem is writable.

---

# CPU & Memory Snapshot

## 5. Check Docker Process Resource Usage

shiv@SHIV:~$ ps -o pid,pcpu,pmem,comm -C dockerd

    PID %CPU %MEM COMMAND
    
    388  1.6  1.6 dockerd
    
Observation:

* Docker daemon consuming low CPU and memory.
* No abnormal resource spikes observed.

## 6. Check Memory Usage

shiv@SHIV:~/90DaysOfDevOps/2026/day-05$ free -h

               total        used        free      shared  buff/cache   available
               
Mem:           7.4Gi       3.9Gi       1.8Gi        50Mi       2.2Gi       3.6Gi

Swap:          2.0Gi        10Mi       2.0Gi

Observation:

* Available memory is sufficient.
* No swap pressure detected.

---

# Disk & IO Snapshot

## 7. Check Disk Space

```bash
df -h
```

Observation:

* Root filesystem utilization below 80%.
* Adequate free space available.

## 8. Check Log Directory Size

```bash
du -sh /var/log
```

Observation:

* Log directory size within acceptable limits.

---

# Network Snapshot

## 9. Check Listening Ports

```bash
ss -tulpn | grep docker
```

Observation:

* Docker-related ports are listening correctly.

## 10. Verify Docker API Response

```bash
docker info
```

Observation:

* Docker daemon responding successfully.
* No communication issues between client and daemon.

---

# Logs Reviewed

## 11. Check Docker Service Logs

```bash
journalctl -u docker -n 50
```

Observation:

* No recent critical errors found.
* Service startup completed successfully.

## 12. Follow Recent System Logs

```bash
tail -n 50 /var/log/syslog
```

Observation:

* No Docker-related failures observed.

---

# Quick Findings

* Docker service is running normally.
* Memory utilization is healthy.
* Disk space is sufficient.
* No recent errors found in logs.
* Network connectivity appears normal.

---

# If This Worsens

### 1. Restart Service

```bash
sudo systemctl restart docker
sudo systemctl status docker
```

### 2. Increase Investigation

```bash
journalctl -u docker --since "1 hour ago"
```

Look for:

* OOM kills
* Permission issues
* Storage driver errors

### 3. Collect Deep Diagnostics

```bash
strace -p <dockerd_pid>
```

or

```bash
docker system events
```

Use when:

* Service hangs
* High CPU usage
* Containers fail unexpectedly

---

# Lessons Learned

Always collect evidence before restarting a service.

Follow the sequence:

CPU → Memory → Disk → Network → Logs → Action

This minimizes guesswork and speeds up incident resolution.

