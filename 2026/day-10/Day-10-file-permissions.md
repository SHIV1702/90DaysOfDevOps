# Day 10 Challenge – File Permissions & File Operations

## Task 1: Create Files

### Commands Used

```bash
touch devops.txt

echo "Linux file permissions practice" > notes.txt

vim script.sh
```

Content of `script.sh`:

```bash
echo "Hello DevOps"
```

Verify permissions:

```bash
ls -l
```

Example Output:

```bash
-rw-rw-r-- 1 user user 0 Jun 12  devops.txt
-rw-rw-r-- 1 user user 31 Jun 12 notes.txt
-rw-rw-r-- 1 user user 19 Jun 12 script.sh
```

---

## Task 2: Read Files

### Read notes.txt

```bash
cat notes.txt
```

### Open script.sh in read-only mode

```bash
vim -R script.sh
```

### Display first 5 lines of /etc/passwd

```bash
head -n 5 /etc/passwd
```

### Display last 5 lines of /etc/passwd

```bash
tail -n 5 /etc/passwd
```

---

## Task 3: Understand Permissions

Permission Format:

```text
rwxrwxrwx
│  │  │
│  │  └── Others
│  └───── Group
└──────── Owner
```

Permission Values:

| Permission  | Value |
| ----------- | ----- |
| Read (r)    | 4     |
| Write (w)   | 2     |
| Execute (x) | 1     |

### Current Permissions

```bash
ls -l devops.txt notes.txt script.sh
```

Example:

```bash
-rw-rw-r-- devops.txt
-rw-rw-r-- notes.txt
-rw-rw-r-- script.sh
```

### Explanation

* Owner: Read + Write
* Group: Read + Write
* Others: Read only
* No execute permission available

---

## Task 4: Modify Permissions

### Make script.sh executable

```bash
chmod +x script.sh
```

Verify:

```bash
ls -l script.sh
```

Output:

```bash
-rwxrwxr-x script.sh
```

Run script:

```bash
./script.sh
```

Output:

```bash
Hello DevOps
```

---

### Set devops.txt to read-only

```bash
chmod a-w devops.txt
```

Verify:

```bash
ls -l devops.txt
```

Output:

```bash
-r--r--r-- devops.txt
```

---

### Set notes.txt permission to 640

```bash
chmod 640 notes.txt
```

Verify:

```bash
ls -l notes.txt
```

Output:

```bash
-rw-r----- notes.txt
```

Meaning:

* Owner: Read + Write
* Group: Read
* Others: No access

---

### Create project directory with 755 permission

```bash
mkdir project
chmod 755 project
```

Verify:

```bash
ls -ld project
```

Output:

```bash
drwxr-xr-x project
```

Meaning:

* Owner: Full access
* Group: Read + Execute
* Others: Read + Execute

---

## Task 5: Test Permissions

### Write to Read-Only File

```bash
echo "test" >> devops.txt
```

Possible Error:

```bash
Permission denied
```

---

### Execute File Without Execute Permission

Remove execute permission:

```bash
chmod -x script.sh
```

Run:

```bash
./script.sh
```

Error:

```bash
Permission denied
```

---

## Commands Used

```bash
touch
echo
cat
vim
vim -R
head
tail
ls -l
chmod
mkdir
./script.sh
```

---

## What I Learned

1. Linux permissions are controlled using read, write, and execute bits.
2. chmod can modify permissions using symbolic and numeric methods.
3. Execute permission is mandatory to run shell scripts.
4. Directories use execute permission for traversal.
5. Proper permissions improve Linux security and access control.
