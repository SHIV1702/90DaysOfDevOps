# File I/O Practice

## Objective

Practice basic file creation, writing, appending, and reading using Linux commands.

### 1. Create a File

devops@SHIV:~$ touch notes.txt

Creates an empty file named `notes.txt`.

### 2. Write Data to the File

```bash
echo "Line 1: Linux File I/O Practice" > notes.txt
echo "Line 2: Using redirection operator" >> notes.txt
echo "Line 3: Using tee command" | tee -a notes.txt
echo "Line 4: Learning file operations" >> notes.txt
echo "Line 5: Reading files with cat" >> notes.txt
echo "Line 6: Using head command" >> notes.txt
echo "Line 7: Using tail command" >> notes.txt
echo "Line 8: DevOps daily practice" >> notes.txt
```

### 3. Read the Entire File

```bash
cat notes.txt
```

Displays all contents of the file.

### 4. Read the First Two Lines

```bash
head -n 2 notes.txt
```

Displays the first two lines.

### 5. Read the Last Two Lines

```bash
tail -n 2 notes.txt
```

Displays the last two lines.

## Notes

* `>` creates/overwrites a file.
* `>>` appends content to a file.
* `tee` writes to a file and displays output on the terminal.
* `cat` reads the complete file.
* `head` shows the beginning of a file.
* `tail` shows the end of a file.
