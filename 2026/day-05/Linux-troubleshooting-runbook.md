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

shiv@SHIV:~/90DaysOfDevOps/2026/day-05$ df -h

Filesystem      Size  Used Avail Use% Mounted on

none            3.8G     0  3.8G   0% /usr/lib/modules/5.15.167.4-microsoft-standard-WSL2

none            3.8G  4.0K  3.8G   1% /mnt/wsl

drivers         476G  446G   31G  94% /usr/lib/wsl/drivers

/dev/sdc       1007G   19G  938G   2% /

none            3.8G   72K  3.8G   1% /mnt/wslg

none            3.8G     0  3.8G   0% /usr/lib/wsl/lib

rootfs          3.8G  2.4M  3.8G   1% /init

none            3.8G  2.0M  3.8G   1% /run

none            3.8G     0  3.8G   0% /run/lock

none            3.8G     0  3.8G   0% /run/shm

tmpfs           4.0M     0  4.0M   0% /sys/fs/cgroup

none            3.8G   96K  3.8G   1% /mnt/wslg/versions.txt

none            3.8G   96K  3.8G   1% /mnt/wslg/doc

C:\             476G  446G   31G  94% /mnt/c

tmpfs           762M   16K  762M   1% /run/user/1000

tmpfs           762M   16K  762M   1% /run/user/1002

Observation:

* Root filesystem utilization below 80%.
* Adequate free space available.

## 8. Check Log Directory Size

shiv@SHIV:/var$ sudo du -sh /var/log

647M    /var/log

Observation:

* Log directory size within acceptable limits.

---

# Network Snapshot

## 9. Check Listening Ports

shiv@SHIV:~$ sudo ss -tulpn | grep docker

tcp   LISTEN 0      4096          0.0.0.0:8080       0.0.0.0:*    users:(("docker-proxy",pid=3077,fd=7))

tcp   LISTEN 0      4096          0.0.0.0:10000      0.0.0.0:*    users:(("docker-proxy",pid=3115,fd=7))

tcp   LISTEN 0      4096          0.0.0.0:32775      0.0.0.0:*    users:(("docker-proxy",pid=2858,fd=7))

tcp   LISTEN 0      4096          0.0.0.0:32774      0.0.0.0:*    users:(("docker-proxy",pid=2823,fd=7))

tcp   LISTEN 0      4096          0.0.0.0:32772      0.0.0.0:*    users:(("docker-proxy",pid=2673,fd=7))

Observation:

* Docker-related ports are listening correctly.

## 10. Verify Docker API Response

shiv@SHIV:~$ sudo docker info

Client:

 Version:    29.1.3
 
 Context:    default
 
 Debug Mode: false
 
 Plugins:
 
 buildx: Docker Buildx (Docker Inc.)
  
 Version:  v0.34.1
    
 Path:     /usr/libexec/docker/cli-plugins/docker-buildx
 
  compose: Docker Compose (Docker Inc.)
  
  Version:  v5.1.4
  
  Path:     /usr/libexec/docker/cli-plugins/docker-compose
  
  trust: Manage trust on Docker images (Docker Inc.)
  
  Version:  29.1.3
  
   Path:     /usr/libexec/docker/cli-plugins/docker-trust

Server:

 Containers: 27
 
  Running: 21
  
  Paused: 0
  
  Stopped: 6
  
 Images: 29
 
 Server Version: 29.1.3
 
Observation:

* Docker daemon responding successfully.
* No communication issues between client and daemon.

---

# Logs Reviewed

## 11. Check Docker Service Logs

shiv@SHIV:~$
shiv@SHIV:~$ sudo journalctl -u docker -n 50

Jun 03 11:35:36 SHIV dockerd[284]: time="2026-06-03T11:35:36.524174486Z" level=error msg="[resolver] 

Jun 03 11:35:36 SHIV dockerd[284]: time="2026-06-03T11:35:36.784453313Z" level=error msg="[resolver] 

Jun 03 11:35:37 SHIV dockerd[284]: time="2026-06-03T11:35:37.237674406Z" level=error msg="[resolver] 

Jun 03 11:35:37 SHIV dockerd[284]: time="2026-06-03T11:35:37.237732271Z" level=error msg="[resolver] 

Jun 03 11:35:37 SHIV dockerd[284]: time="2026-06-03T11:35:37.280226426Z" level=error msg="[resolver] 

Jun 03 11:35:37 SHIV dockerd[284]: time="2026-06-03T11:35:37.280243224Z" level=error msg="[resolver] 

Observation:

* No recent critical errors found.
* Service startup completed successfully.

## 12. Follow Recent System Logs

shiv@SHIV:~$ sudo tail -n 50 /var/log/syslog

2026-06-03T11:38:00.557837+00:00 SHIV dockerd[284]: time="2026-06-03T11:38:00.557604643Z" level=error msg="[resolver] failed to query external DNS server" client-addr="udp:10.255.255.254:58071" dns-server="udp:10.255.255.254:53" error="read udp 10.255.255.254:58071->10.255.255.254:53: i/o timeout" question=";otel-collector.\tIN\t AAAA"

2026-06-03T11:38:00.829779+00:00 SHIV dockerd[284]: time="2026-06-03T11:38:00.829466780Z" level=error msg="[resolver] failed to query external DNS server" client-addr="udp:10.255.255.254:59636" dns-server="udp:10.255.255.254:53" error="read udp 10.255.255.254:59636->10.255.255.254:53: i/o timeout" question=";otel-collector.\tIN\t A"

2026-06-03T11:38:01.475752+00:00 SHIV dockerd[284]: time="2026-06-03T11:38:01.475002091Z" level=error msg="[resolver] failed to query external DNS server" client-addr="udp:10.255.255.254:34328" dns-server="udp:10.255.255.254:53" error="read udp 10.255.255.254:34328->10.255.255.254:53: 

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

sudo systemctl restart docker
sudo systemctl status docker


### 2. Increase Investigation

journalctl -u docker --since "1 hour ago"


Look for:

* OOM kills
* Permission issues
* Storage driver errors

### 3. Collect Deep Diagnostics

strace -p <dockerd_pid>

or

docker system events


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

