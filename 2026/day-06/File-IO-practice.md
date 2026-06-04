# File I/O Practice

## Objective

Practice basic file creation, writing, appending, and reading using Linux commands.

### 1. Create a File

devops@SHIV:~$ touch notes.txt

Creates an empty file named `notes.txt`.

### 2. Write Data to the File

devops@SHIV:~$ echo "This is 90DaysOfDevops day-05">notes.txt

devops@SHIV:~$ echo "Today I am practicing linux">>notes.txt

devops@SHIV:~$ echo "I performing an opertaion of editing a file by overwriting and appending it in the created file"|tee -a notes.txt

I performing an opertaion of editing a file by overwriting and appending it in the created file

### 3. Read the Entire File

devops@SHIV:~$ cat notes.txt

This is 90DaysOfDevops day-05

Today I am practicing linux

I performing an opertaion of editing a file by overwriting and appending it in the created file

Displays all contents of the file.

### 4. Read the First Two Lines

devops@SHIV:~$ head -n 2 notes.txt

This is 90DaysOfDevops day-05

Today I am practicing linux

devops@SHIV:~$

Displays the first two lines.

### 5. Read the Last Two Lines

devops@SHIV:~$ tail -n 2 notes.txt

Today I am practicing linux

I performing an opertaion of editing a file by overwriting and appending it in the created file

devops@SHIV:~$

Displays the last two lines.

## Notes

* `>` creates/overwrites a file.
* `>>` appends content to a file.
* `tee` writes to a file and displays output on the terminal.
* `cat` reads the complete file.
* `head` shows the beginning of a file.
* `tail` shows the end of a file.
