# Linux File Permissions

## What are Linux File Permissions?

Linux permissions control **who can read, write, or execute** a file or directory.

Permissions are assigned to:

- **Owner (User)**
- **Group**
- **Others**

---

## Permission Types

| Permission | Symbol | Value | Meaning                                           |
| ---------- | -----: | ----: | ------------------------------------------------- |
| Read       |    `r` |     4 | Read file / list directory                        |
| Write      |    `w` |     2 | Modify file / create or delete files in directory |
| Execute    |    `x` |     1 | Run file / access directory                       |

---

## Permission Structure

```text
-rwxr-xr--
 │││ │││ │││
 │││ │││ └── Others
 │││ └────── Group
 └────────── Owner
```

Example:

```text
-rwxr-xr--
```

- **Owner:** `rwx`
- **Group:** `r-x`
- **Others:** `r--`

---

## View Permissions

```bash
ls -l
```

Example:

```text
-rwxr-xr-- 1 ubuntu developers 2048 file.sh
```

---

# `chmod` — Change Permissions

Syntax:

```bash
chmod permissions file
```

### Symbolic Mode

```bash
chmod +x script.sh
chmod -w file.txt
chmod u+rw file.txt
chmod g+x script.sh
chmod o-rwx file.txt
```

Where:

```text
u → User/Owner
g → Group
o → Others
a → All
```

---

# Numeric Permissions

```text
r = 4
w = 2
x = 1
```

| Number | Permission |
| -----: | ---------- |
|    `7` | `rwx`      |
|    `6` | `rw-`      |
|    `5` | `r-x`      |
|    `4` | `r--`      |
|    `0` | `---`      |

### Common Examples

```bash
chmod 755 script.sh
chmod 644 file.txt
chmod 600 private.key
```

| Permission | Meaning     | Common Use                                     |
| ---------- | ----------- | ---------------------------------------------- |
| `755`      | `rwxr-xr-x` | Scripts, directories                           |
| `644`      | `rw-r--r--` | Regular/config files                           |
| `600`      | `rw-------` | Private/sensitive files                        |
| `777`      | `rwxrwxrwx` | Full access for everyone — avoid when possible |

---

# `chown` — Change Owner

```bash
sudo chown ubuntu file.txt
```

Change owner and group:

```bash
sudo chown ubuntu:developers file.txt
```

---

# `chgrp` — Change Group

```bash
sudo chgrp developers file.txt
```

---

# Directory Permissions

Directory permissions work differently:

| Permission | Directory Meaning            |
| ---------- | ---------------------------- |
| `r`        | List contents                |
| `w`        | Create, delete, rename files |
| `x`        | Enter/access directory       |

Example:

```bash
chmod 755 project/
```

---

# Recursive Permissions

Apply permissions to a directory and its contents:

```bash
chmod -R 755 project/
```

Change ownership recursively:

```bash
sudo chown -R ubuntu:developers project/
```

> Use recursive commands carefully, especially on production systems.

---

# Special Permissions

### SUID

Runs a program with the owner's privileges.

```bash
chmod u+s program
```

Example:

```text
-rwsr-xr-x
```

### SGID

Allows files in a directory to inherit its group.

```bash
chmod g+s directory
```

### Sticky Bit

Prevents users from deleting files they do not own in a shared directory.

```bash
chmod +t /shared
```

Example:

```text
drwxrwxrwt
```

Commonly used on `/tmp`.

---

# `stat` — Detailed Information

```bash
stat file.txt
```

Shows:

- Permissions
- Owner
- Group
- Size
- Inode
- Timestamps

---

# Important Commands

| Command | Purpose                          |
| ------- | -------------------------------- |
| `ls -l` | View permissions                 |
| `chmod` | Change permissions               |
| `chown` | Change owner                     |
| `chgrp` | Change group                     |
| `stat`  | View detailed file information   |
| `umask` | View default permission settings |

---

# Common Use Cases

- Make scripts executable
- Secure SSH private keys
- Control application access
- Manage shared directories
- Protect configuration files
- Secure sensitive data

---

# Best Practices

- Use **644** for normal files.
- Use **755** for executable scripts and directories.
- Use **600** for private keys and sensitive files.
- Avoid **777** unless absolutely necessary.
- Follow the **principle of least privilege**.
- Be careful with recursive `chmod` and `chown`.

---

## Why Learn Linux File Permissions?

File permissions are a fundamental part of **Linux security and administration**. Understanding `chmod`, `chown`, and `chgrp` helps you control access, secure applications, and manage production Linux servers.
