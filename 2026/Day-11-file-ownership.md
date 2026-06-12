# Day 11 Challenge – File Ownership (chown & chgrp)

## Files & Directories Created

### Files

* devops-file.txt
* team-notes.txt
* project-config.yaml
* heist-project/vault/gold.txt
* heist-project/plans/strategy.conf
* bank-heist/access-codes.txt
* bank-heist/blueprints.pdf
* bank-heist/escape-plan.txt

### Directories

* app-logs/
* heist-project/
* heist-project/vault/
* heist-project/plans/
* bank-heist/

### Users

* tokyo
* berlin
* professor
* nairobi

### Groups

* heist-team
* planners
* vault-team
* tech-team

---

## Task 1: Understanding Ownership

### Check File Ownership

```bash
ls -l
```

Example Output:

```bash
-rw-r--r-- 1 devops devops 0 Jun 13 devops-file.txt
```

### Ownership Format

```text
-rw-r--r--
│
├── Owner → devops
└── Group → devops
```

### Difference Between Owner and Group

* Owner is the user who has primary control over a file or directory.
* Group is a collection of users who can share access to files.
* Linux permissions are applied separately to Owner, Group, and Others.

---

## Task 2: Basic chown Operations

### Create File

```bash
touch devops-file.txt
```

### Verify Current Owner

```bash
ls -l devops-file.txt
```

### Change Owner to Tokyo

```bash
sudo chown tokyo devops-file.txt
```

### Verify

```bash
ls -l devops-file.txt
```

### Change Owner to Berlin

```bash
sudo chown berlin devops-file.txt
```

### Verify Again

```bash
ls -l devops-file.txt
```

### Ownership Changes

| File            | Before        | After         |
| --------------- | ------------- | ------------- |
| devops-file.txt | devops:devops | tokyo:devops  |
| devops-file.txt | tokyo:devops  | berlin:devops |

---

## Task 3: Basic chgrp Operations

### Create File

```bash
touch team-notes.txt
```

### Create Group

```bash
sudo groupadd heist-team
```

### Change Group

```bash
sudo chgrp heist-team team-notes.txt
```

### Verify

```bash
ls -l team-notes.txt
```

### Result

```text
devops:devops → devops:heist-team
```

---

## Task 4: Combined Owner & Group Change

### Create File

```bash
touch project-config.yaml
```

### Change Owner and Group Together

```bash
sudo chown professor:heist-team project-config.yaml
```

### Verify

```bash
ls -l project-config.yaml
```

### Create Directory

```bash
mkdir app-logs
```

### Change Owner and Group

```bash
sudo chown berlin:heist-team app-logs
```

### Verify

```bash
ls -ld app-logs
```

---

## Task 5: Recursive Ownership

### Create Directory Structure

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans

touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

### Create Group

```bash
sudo groupadd planners
```

### Apply Recursive Ownership

```bash
sudo chown -R professor:planners heist-project
```

### Verify

```bash
ls -lR heist-project
```

### Result

All files and directories under heist-project are now owned by:

```text
Owner : professor
Group : planners
```

---

## Task 6: Practice Challenge

### Create Users

```bash
sudo useradd tokyo
sudo useradd berlin
sudo useradd nairobi
```

### Create Groups

```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

### Create Directory and Files

```bash
mkdir bank-heist

touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

### Assign Ownership

```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt

sudo chown berlin:tech-team bank-heist/blueprints.pdf

sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

### Verify

```bash
ls -l bank-heist
```

### Final Ownership

| File             | Owner   | Group      |
| ---------------- | ------- | ---------- |
| access-codes.txt | tokyo   | vault-team |
| blueprints.pdf   | berlin  | tech-team  |
| escape-plan.txt  | nairobi | vault-team |

---

## Commands Used

```bash
ls -l
ls -ld
ls -lR
touch
mkdir
sudo useradd
sudo groupadd
sudo chown
sudo chgrp
sudo chown -R
```

---

## Troubleshooting

### Permission Denied

Use sudo while changing ownership:

```bash
sudo chown username filename
```

### User Does Not Exist

Create user first:

```bash
sudo useradd username
```

### Group Does Not Exist

Create group first:

```bash
sudo groupadd groupname
```

---

## What I Learned

1. Every file and directory in Linux has an owner and an associated group.
2. chown can change both owner and group in a single command.
3. Recursive ownership changes using `-R` are useful for application and project directories.
4. Ownership and permissions work together to control file access.
5. Proper ownership management is critical for DevOps tasks such as deployments, shared environments, container permissions, CI/CD artifacts, and log management.

---

## Why This Matters for DevOps

Proper file ownership is essential for:

* Application deployments
* Shared team directories
* Container file permissions
* CI/CD pipeline artifacts
* Log file management
* Kubernetes persistent volumes
* Secure access control in Linux environments
