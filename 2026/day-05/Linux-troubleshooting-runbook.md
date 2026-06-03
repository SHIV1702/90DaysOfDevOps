# Linux Troubleshooting Runbook

## Target Service / Process

Service: Docker

Purpose: Verify Docker daemon health and collect system resource information before taking corrective action.

---

# Environment Basics

## 1. Check Kernel Information

```bash
uname -a
```

Observation:

* Ubuntu Linux kernel is running normally.
* No immediate OS-level issues detected.

## 2. Check OS Version

```bash
cat /etc/os-release
```

Observation:

* Ubuntu 24.04 LTS confirmed.

---

# Filesystem Sanity

## 3. Create Test Directory

```bash
mkdir -p /tmp/runbook-demo
```

Observation:

* Directory created successfully.

## 4. Copy and Verify File

```bash
cp /etc/hosts /tmp/runbook-demo/hosts-copy
ls -l /tmp/runbook-demo
```

Observation:

* File copied successfully.
* Filesystem is writable.

---

# CPU & Memory Snapshot

## 5. Check Docker Process Resource Usage

```bash
ps -o pid,pcpu,pmem,comm -C dockerd
```

Observation:

* Docker daemon consuming low CPU and memory.
* No abnormal resource spikes observed.

## 6. Check Memory Usage

```bash
free -h
```

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

