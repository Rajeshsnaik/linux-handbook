# `chown` — Change File Ownership

`chown` stands for **Change Owner**.

It is used to change the **owner and/or group ownership** of files and directories in Linux.

Linux permissions are based on three ownership categories:

- **User (Owner)**
- **Group**
- **Others**

The `chown` command allows you to change the **user owner**, **group owner**, or both.

---

## Basic Command

```bash
chown <user> <file>
```

Example:

```bash
chown rajesh file.txt
```

This changes the owner of `file.txt` to `rajesh`.

Check the ownership:

```bash
ls -l file.txt
```

Example:

```text
-rw-r--r-- 1 rajesh developers 1024 Aug 21 file.txt
```

---

## Change Owner and Group

```bash
chown <user>:<group> <file>
```

Example:

```bash
chown rajesh:developers file.txt
```

Now:

```text
Owner → rajesh
Group → developers
```

---

## Change Only Group

You can change only the group using:

```bash
chown :<group> <file>
```

Example:

```bash
chown :developers file.txt
```

Or use:

```bash
chgrp developers file.txt
```

---

# Change Ownership of a Directory

```bash
chown rajesh project/
```

This changes the owner of the directory itself.

Check:

```bash
ls -ld project/
```

---

# Recursive Ownership Change

To change ownership of a directory **and everything inside it**:

```bash
chown -R rajesh:developers project/
```

`-R` means **recursive**.

Example:

```text
project/
├── app.js
├── config/
│   └── app.conf
└── logs/
    └── app.log
```

Running:

```bash
chown -R rajesh:developers project/
```

changes ownership of:

```text
project/
app.js
config/
app.conf
logs/
app.log
```

---

# Change Owner Only

```bash
chown rajesh file.txt
```

Changes:

```text
Owner → rajesh
Group → unchanged
```

---

# Change Group Only

```bash
chown :developers file.txt
```

Changes:

```text
Owner → unchanged
Group → developers
```

---

# Change Owner and Group

```bash
chown rajesh:developers file.txt
```

Changes:

```text
Owner → rajesh
Group → developers
```

---

# Using User and Group IDs

`chown` can also work with numeric UID and GID.

```bash
chown 1001:1001 file.txt
```

This sets:

```text
UID → 1001
GID → 1001
```

Check:

```bash
ls -ln file.txt
```

The `-n` option displays numeric UID/GID instead of names.

---

# Verify Ownership

### Using `ls -l`

```bash
ls -l file.txt
```

Example:

```text
-rw-r--r-- 1 rajesh developers 1024 Aug 21 file.txt
```

Here:

```text
rajesh     → Owner
developers → Group
```

### Using `stat`

```bash
stat file.txt
```

Example:

```text
Uid: (1001/rajesh)
Gid: (1002/developers)
```

---

# `chown` with `sudo`

Changing ownership of system files usually requires root privileges.

```bash
sudo chown rajesh:developers file.txt
```

For a directory:

```bash
sudo chown -R rajesh:developers /opt/project
```

---

# Useful Options

| Option        | Meaning                                  |
| ------------- | ---------------------------------------- |
| `-R`          | Recursive                                |
| `-v`          | Verbose output                           |
| `-c`          | Report only when a change is made        |
| `-h`          | Change ownership of symbolic link itself |
| `--reference` | Use ownership from another file          |

---

## Verbose Mode

```bash
chown -v rajesh:developers file.txt
```

Shows what ownership changes were made.

---

## Change Ownership Based on Another File

```bash
chown --reference=file1.txt file2.txt
```

The ownership of `file2.txt` becomes the same as `file1.txt`.

---

# `chown` and Symbolic Links

Consider:

```text
app.log → /var/log/application.log
```

Normally:

```bash
chown rajesh app.log
```

may operate on the target of the symbolic link depending on the command behavior and platform.

To change the ownership of the **symbolic link itself**, use:

```bash
chown -h rajesh app.log
```

---

# Real-World Example

Suppose an application is deployed under:

```text
/var/www/myapp
```

The files were accidentally created by `root`:

```text
root root
```

Your application user is:

```text
www-data
```

You can change ownership:

```bash
sudo chown -R www-data:www-data /var/www/myapp
```

Verify:

```bash
ls -l /var/www/myapp
```

Now the application files are owned by:

```text
www-data:www-data
```

This is commonly seen with **Nginx, Apache, PHP applications, and web deployments**.

---

# `chown` vs `chmod`

These commands solve different problems.

| `chown`                    | `chmod`                                 |
| -------------------------- | --------------------------------------- |
| Changes ownership          | Changes permissions                     |
| Changes user/group         | Changes `rwx` permissions               |
| `chown user:group file`    | `chmod 755 file`                        |
| Controls who owns the file | Controls what owner/group/others can do |

Example:

```bash
chown rajesh:developers app.log
chmod 640 app.log
```

Result:

```text
Owner  → rajesh
Group  → developers
Mode   → rw-r-----
```

---

# `chown` vs `chgrp`

### `chown`

Can change:

- Owner
- Group
- Owner + Group

```bash
chown rajesh:developers file.txt
```

### `chgrp`

Changes only the group:

```bash
chgrp developers file.txt
```

---

# Important Points

- `chown` means **Change Owner**.
- It can change the **user owner**.
- It can change the **group owner**.
- `chown user:group file` changes both.
- `-R` applies the change recursively.
- `sudo` is commonly required for files you do not own.
- `ls -l` and `stat` can be used to verify ownership.
- `chown` changes ownership; `chmod` changes permissions.

---

# Quick Reference

```bash
chown user file                    # Change owner
chown user:group file              # Change owner and group
chown :group file                  # Change group only
chown -R user:group directory      # Recursive ownership change
chown -v user:group file           # Verbose output
chown --reference=file1 file2      # Copy ownership
chown 1001:1001 file               # Use UID/GID
chown -h user symlink               # Change symlink ownership
ls -l file                         # Check ownership
stat file                          # Detailed ownership information
```

> **Interview Point:** `chown` changes the **ownership of files and directories**, while `chmod` changes their **permissions**. The common syntax `chown user:group file` changes both the owner and group.
