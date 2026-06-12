# Day 09 - Linux User & Group Management Challenge

## Objective

The goal of this challenge was to gain hands-on experience with Linux user management, group management, permissions, and shared directory access. 

---

# Users & Groups Created

## Users

* tokyo
* berlin
* professor
* nairobi

## Groups

* developers
* admins
* project-team

---

# Group Assignments

| User      | Groups                   |
| --------- | ------------------------ |
| tokyo     | developers, project-team |
| berlin    | developers, admins       |
| professor | admins                   |
| nairobi   | project-team             |

---

# Directories Created

| Directory           | Group Owner  | Permissions |
| ------------------- | ------------ | ----------- |
| /opt/dev-project    | developers   | 775         |
| /opt/team-workspace | project-team | 775         |

---

# Commands Used

## Task 1 - Create Users

Create users with home directories:

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m professor
```

Set passwords:

```bash
sudo passwd tokyo
sudo passwd berlin
sudo passwd professor
```

Verify users:

```bash
cat /etc/passwd | grep -E "tokyo|berlin|professor"
ls -l /home
```

---

## Task 2 - Create Groups

Create groups:

```bash
sudo groupadd developers
sudo groupadd admins
```

Verify:

```bash
cat /etc/group | grep -E "developers|admins"
```

---

## Task 3 - Assign Users to Groups

Add tokyo to developers:

```bash
sudo usermod -aG developers tokyo
```

Add berlin to developers and admins:

```bash
sudo usermod -aG developers berlin
sudo usermod -aG admins berlin
```

Add professor to admins:

```bash
sudo usermod -aG admins professor
```

Verify memberships:

```bash
groups tokyo
groups berlin
groups professor
```

Expected Output:

```text
tokyo : tokyo developers

berlin : berlin developers admins

professor : professor admins
```

---

## Task 4 - Shared Directory

Create directory:

```bash
sudo mkdir -p /opt/dev-project
```

Assign group ownership:

```bash
sudo chgrp developers /opt/dev-project
```

Set permissions:

```bash
sudo chmod 775 /opt/dev-project
```

Verify:

```bash
ls -ld /opt/dev-project
```

Expected:

```text
drwxrwxr-x
```

Create files as users:

```bash
sudo -u tokyo touch /opt/dev-project/tokyo.txt

sudo -u berlin touch /opt/dev-project/berlin.txt
```

Verify:

```bash
ls -l /opt/dev-project
```

Expected:

```text
tokyo.txt
berlin.txt
```

---

## Task 5 - Team Workspace

Create user:

```bash
sudo useradd -m nairobi
sudo passwd nairobi
```

Create group:

```bash
sudo groupadd project-team
```

Add users:

```bash
sudo usermod -aG project-team tokyo
sudo usermod -aG project-team nairobi
```

Verify:

```bash
groups tokyo
groups nairobi
```

Create directory:

```bash
sudo mkdir -p /opt/team-workspace
```

Assign group:

```bash
sudo chgrp project-team /opt/team-workspace
```

Set permissions:

```bash
sudo chmod 775 /opt/team-workspace
```

Verify:

```bash
ls -ld /opt/team-workspace
```

Create file as nairobi:

```bash
sudo -u nairobi touch /opt/team-workspace/nairobi.txt
```

Verify:

```bash
ls -l /opt/team-workspace
```

---

# Verification Commands

Verify users:

```bash
cat /etc/passwd | grep -E "tokyo|berlin|professor|nairobi"
```

Verify groups:

```bash
cat /etc/group | grep -E "developers|admins|project-team"
```

Verify memberships:

```bash
groups tokyo
groups berlin
groups professor
groups nairobi
```

Verify directories:

```bash
ls -ld /opt/dev-project
ls -ld /opt/team-workspace
```

Verify files:

```bash
ls -l /opt/dev-project
ls -l /opt/team-workspace
```

---

# Screenshots Taken

1. User creation
2. Group creation
3. Group membership verification
4. /opt/dev-project permissions
5. File creation by tokyo and berlin
6. /opt/team-workspace permissions
7. File creation by nairobi

---

# What I Learned

* Linux users and groups are used to control access to resources.
* Group-based permissions simplify collaboration among multiple users.
* The `usermod -aG` command is used to add users to supplementary groups.
* The `chmod` command controls file and directory permissions.
* The `chgrp` command changes group ownership of files and directories.
* Shared directories are commonly used in development and operations teams.

---

# Real-World DevOps Relevance

User and group management is an essential DevOps skill because:

* Teams need controlled access to servers.
* CI/CD tools often run under dedicated service accounts.
* Shared project directories require proper permissions.
* Security best practices rely on least-privilege access.
* Production systems use groups to manage access efficiently.
