# Types of Files in Linux

## What are File Types in Linux?

In Linux, **everything is treated as a file**, including regular files, directories, devices, pipes, and sockets.

You can identify file types using:

```bash
ls -l
file filename
stat filename
```

---

## File Types

| Symbol | File Type         | Purpose                                              |
| ------ | ----------------- | ---------------------------------------------------- |
| `-`    | Regular File      | Stores text, images, scripts, programs, etc.         |
| `d`    | Directory         | Stores files and directories.                        |
| `l`    | Symbolic Link     | Shortcut/reference to another file or directory.     |
| `c`    | Character Device  | Transfers data character by character.               |
| `b`    | Block Device      | Transfers data in blocks; commonly used for storage. |
| `p`    | Named Pipe (FIFO) | Enables communication between processes.             |
| `s`    | Socket            | Enables communication between processes/services.    |

---

## 1. Regular File (`-`)

Stores normal user or application data.

Examples:

```text
notes.txt
script.sh
photo.jpg
app.py
```

Create:

```bash
touch file.txt
```

Example:

```text
-rw-r--r-- file.txt
```

---

## 2. Directory (`d`)

Used to organize files and other directories.

Create:

```bash
mkdir project
```

Example:

```text
drwxr-xr-x project/
```

---

## 3. Symbolic Link (`l`)

A symbolic link is a shortcut that points to another file or directory.

Create:

```bash
ln -s file.txt link.txt
```

Example:

```text
lrwxrwxrwx link.txt -> file.txt
```

---

## 4. Character Device (`c`)

Transfers data one character at a time.

Examples:

```text
/dev/tty
/dev/null
/dev/random
```

Check:

```bash
ls -l /dev/tty
```

---

## 5. Block Device (`b`)

Transfers data in blocks and is commonly used for storage devices.

Examples:

```text
/dev/sda
/dev/nvme0n1
```

Check:

```bash
ls -l /dev/sda
```

---

## 6. Named Pipe / FIFO (`p`)

Used for communication between processes.

Create:

```bash
mkfifo mypipe
```

Check:

```bash
ls -l mypipe
```

---

## 7. Socket (`s`)

Used for communication between processes and services.

Examples:

```text
Docker socket
Database socket
Web server socket
```

Find sockets:

```bash
find /run -type s
```

---

## Identify File Types

### Using `ls -l`

```bash
ls -l
```

The **first character** shows the file type.

```text
-rw-r--r--  → Regular file
drwxr-xr-x  → Directory
lrwxrwxrwx  → Symbolic link
```

### Using `file`

```bash
file filename
```

### Using `stat`

```bash
stat filename
```

Displays detailed information such as:

- File type
- Size
- Permissions
- Inode
- Timestamps

---

## Example

```text
-rw-r--r--  file.txt
drwxr-xr-x  project/
lrwxrwxrwx  link -> file.txt
crw-rw-rw-  /dev/null
brw-rw----  /dev/sda
prw-r--r--  mypipe
srwxrwxrwx  docker.sock
```

The **first character identifies the file type**.

---

## Common Use Cases

- Store application data
- Organize files using directories
- Create shortcuts using symbolic links
- Access hardware through device files
- Enable process communication
- Work with storage devices
- Troubleshoot Linux systems

---

## Why Learn File Types?

Understanding Linux file types is important for **Linux administration, DevOps, cloud computing, and troubleshooting**. It helps you understand how Linux represents everything from normal files and directories to **devices, processes, and services**.
