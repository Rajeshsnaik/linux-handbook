# `umask` — User File-Creation Mask

`umask` stands for **User File-Creation Mask**.

It controls the **default permissions** assigned to newly created files and directories.

It does **not directly set permissions**. Instead, it removes permissions from the default permissions used when a file or directory is created.

---

## Basic Command

```bash
umask
```

Example:

```text
0022
```

This means the current user's default creation mask is `022`.

---

## Default Permissions

Linux starts with these maximum permissions when creating new objects:

### Files

```text
666
```

Equivalent to:

```text
rw-rw-rw-
```

Files do **not** get execute permission by default.

### Directories

```text
777
```

Equivalent to:

```text
rwxrwxrwx
```

---

## How `umask` Works

The basic idea is:

```text
File permissions      666
umask                  022
--------------------------
Result                 644
```

So a new file normally becomes:

```text
-rw-r--r--
```

For directories:

```text
Directory permissions 777
umask                  022
--------------------------
Result                 755
```

So a new directory normally becomes:

```text
drwxr-xr-x
```

> **Important:** `umask` is better understood as a **permission mask**, rather than simple arithmetic subtraction. The kernel applies the mask to the permission bits.

---

# Check Current `umask`

```bash
umask
```

Example:

```text
0022
```

You can also use:

```bash
umask -S
```

Example:

```text
u=rwx,g=rx,o=rx
```

`-S` displays the mask in **symbolic format**.

---

# Common `umask` Values

| umask | New File | New Directory |
| ----- | -------- | ------------- |
| `000` | `666`    | `777`         |
| `002` | `664`    | `775`         |
| `022` | `644`    | `755`         |
| `027` | `640`    | `750`         |
| `077` | `600`    | `700          |

---

# Set `umask`

### Set `umask` to `022`

```bash
umask 022
```

Now:

```bash
touch file.txt
mkdir test
```

Check:

```bash
ls -l
```

You will typically get:

```text
-rw-r--r-- file.txt
drwxr-xr-x test
```

---

# `umask 002`

```bash
umask 002
```

New files:

```text
664
```

New directories:

```text
775
```

This is commonly useful in **shared development environments** where users need group write access.

Example:

```text
File       → rw-rw-r--
Directory  → rwxrwxr-x
```

---

# `umask 077`

```bash
umask 077
```

New files:

```text
600
```

New directories:

```text
700
```

This provides more restrictive permissions.

Example:

```text
File       → rw-------
Directory  → rwx------
```

Useful when newly created files/directories should be accessible only by the owner.

---

# Symbolic `umask`

You can also set the mask using symbolic notation:

```bash
umask u=rwx,g=rx,o=
```

Check:

```bash
umask -S
```

Example:

```text
u=rwx,g=rx,o=
```

---

# Temporary vs Permanent `umask`

Running:

```bash
umask 027
```

changes the `umask` for the **current shell session** and processes started from it.

To make it persistent, configure it in the appropriate shell startup or login configuration.

For Bash, commonly:

```bash
~/.bashrc
```

or:

```bash
~/.profile
```

For a system-wide configuration, the exact file depends on the Linux distribution and login mechanism.

Example:

```bash
umask 027
```

After changing the configuration, start a new session or reload the relevant configuration.

---

# Check File Permissions with `umask`

Example:

```bash
umask 022
touch example.txt
mkdir example
```

Check:

```bash
ls -ld example.txt example
```

Expected result:

```text
-rw-r--r-- example.txt
drwxr-xr-x example
```

Why?

```text
File:
666 → 644

Directory:
777 → 755
```

---

# `umask` and `chmod`

These commands have different purposes.

### `umask`

Controls the **default permissions for newly created files/directories**.

```bash
umask 027
```

### `chmod`

Changes permissions of an **existing file or directory**.

```bash
chmod 640 file.txt
```

Example:

```text
umask → controls default permissions
chmod → changes existing permissions
```

---

# `umask` vs ACL

| `umask`                                 | ACL                                |
| --------------------------------------- | ---------------------------------- |
| Controls default permissions            | Provides fine-grained permissions  |
| Applies when creating objects           | Applies to specific users/groups   |
| Does not directly modify existing files | Can modify access rules            |
| Useful for default security             | Useful for advanced access control |

---

# Real-World Example

Suppose a DevOps server has multiple developers working on:

```text
/opt/project
```

You want newly created files to be:

```text
rw-rw-r--
```

and directories:

```text
rwxrwxr-x
```

Set:

```bash
umask 002
```

Now:

```bash
touch app.log
mkdir logs
```

Typically:

```text
app.log → 664
logs    → 775
```

This allows the owner and group to work with the newly created resources.

---

# Important Points

- `umask` controls **default permissions**.
- Files start from a maximum of **`666`**.
- Directories start from a maximum of **`777`**.
- Files normally don't receive execute permission from creation defaults.
- `umask 022` commonly results in files `644` and directories `755`.
- `umask 077` provides owner-only defaults.
- `umask` affects newly created files/directories, not existing ones.
- `chmod` is used to change permissions after creation.
- `umask` can be configured for shell/user/system environments depending on how processes are started.

---

# Quick Reference

```bash
umask                  # Show current umask
umask -S               # Show symbolic umask
umask 022              # Set umask
umask 002              # Group-friendly default
umask 027              # More restrictive default
umask 077              # Owner-only default
```

### Common Results

```text
umask 022
File       → 644
Directory  → 755

umask 002
File       → 664
Directory  → 775

umask 027
File       → 640
Directory  → 750

umask 077
File       → 600
Directory  → 700
```

> **Interview Point:** `umask` controls the **default permissions of newly created files and directories** by masking out permission bits from the system's default creation permissions. For files, the starting maximum is typically `666`; for directories, it is `777`.
