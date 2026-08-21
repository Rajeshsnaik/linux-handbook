# Linux ACL — Access Control Lists

**ACL (Access Control List)** provides more granular file and directory permissions than the traditional Linux `rwx` permissions.

Normally, Linux permissions are defined for:

- **User (Owner)**
- **Group**
- **Others**

ACL allows you to give permissions to **specific users or groups** without changing the existing owner/group.

---

## Why Use ACL?

Suppose:

```text
file.txt
Owner  → rajesh
Group  → developers
```

You want to give another user, `john`, read access without changing the owner or group.

With normal permissions, this can be difficult.

With ACL:

```bash
setfacl -m u:john:r file.txt
```

Now `john` can read the file.

---

## Check ACL

### `getfacl`

```bash
getfacl file.txt
```

Displays the ACL entries of a file.

Example:

```text
# file: file.txt
# owner: rajesh
# group: developers
user::rw-
user:john:r--
group::r--
mask::r--
other::---
```

---

## Set ACL

### Give a User Permission

```bash
setfacl -m u:<username>:<permissions> <file>
```

Example:

```bash
setfacl -m u:john:rwx file.txt
```

Gives `john`:

```text
read + write + execute
```

---

### Give Read Permission

```bash
setfacl -m u:john:r file.txt
```

---

### Give Read and Write Permission

```bash
setfacl -m u:john:rw file.txt
```

---

### Give a Group Permission

```bash
setfacl -m g:<group-name>:<permissions> <file>
```

Example:

```bash
setfacl -m g:developers:rw file.txt
```

---

## Remove ACL

### Remove a User ACL

```bash
setfacl -x u:john file.txt
```

Removes the specific ACL entry for `john`.

---

### Remove a Group ACL

```bash
setfacl -x g:developers file.txt
```

---

### Remove All ACL Entries

```bash
setfacl -b file.txt
```

Removes all extended ACL entries and returns the file to normal Linux permission behavior.

---

## ACL on Directories

ACL can also be applied to directories.

```bash
setfacl -m u:john:rwx /project
```

This gives `john` permissions on the directory.

---

## Default ACL

A **default ACL** is used on directories so that newly created files and directories inherit the specified ACL.

Example:

```bash
setfacl -d -m u:john:rwx /project
```

Check it:

```bash
getfacl /project
```

You may see:

```text
default:user::rwx
default:user:john:rwx
default:group::r-x
default:mask::rwx
default:other::---
```

This is commonly useful for **shared project directories**.

---

## ACL Mask

The **ACL mask** defines the maximum effective permissions for:

- Named users
- Named groups
- The owning group

Example:

```bash
setfacl -m u:john:rwx,m:rx file.txt
```

Although `john` is assigned `rwx`, the mask limits the effective permissions to:

```text
r-x
```

Check the effective permission with:

```bash
getfacl file.txt
```

Example:

```text
user:john:rwx                #effective:r-x
```

---

## Recursive ACL

To apply ACL to a directory and its existing contents:

```bash
setfacl -R -m u:john:rwx /project
```

`-R` means **recursive**.

---

## Recursive Default ACL

For a shared directory where new files should inherit permissions:

```bash
setfacl -R -m u:john:rwx /project
setfacl -d -m u:john:rwx /project
```

---

## Copy ACL

You can copy ACL permissions from one file to another.

```bash
getfacl file1.txt | setfacl --set-file=- file2.txt
```

---

## Backup ACL

Save ACL information:

```bash
getfacl -R /project > acl_backup.txt
```

Restore ACL:

```bash
setfacl --restore=acl_backup.txt
```

---

## Identify ACL-Enabled Files

When using `ls -l`, a file with an extended ACL usually has a `+` after the permission bits.

```bash
ls -l file.txt
```

Example:

```text
-rw-rw-r--+ 1 rajesh developers 1024 Aug 21 file.txt
```

The `+` indicates that the file has **extended ACL entries**.

---

## Common ACL Permissions

| Permission | Meaning                |
| ---------- | ---------------------- |
| `r`        | Read                   |
| `w`        | Write                  |
| `x`        | Execute                |
| `rw`       | Read + Write           |
| `rwx`      | Read + Write + Execute |
| `---`      | No permission          |

---

## ACL vs Normal Linux Permissions

| Normal Permissions                | ACL                                |
| --------------------------------- | ---------------------------------- |
| Owner                             | Owner                              |
| Group                             | Group                              |
| Others                            | Others                             |
| Limited to basic user/group model | Supports specific users and groups |
| `chmod`                           | `setfacl`                          |
| `ls -l`                           | `getfacl`                          |
| Simple permission management      | Fine-grained permission management |

---

## Real-World Example

Suppose `/app` is a shared application directory.

```text
/app
├── config
├── logs
├── scripts
└── data
```

The owner is:

```text
root
```

You want:

- `devops` → full access
- `developer` → read/write access
- `auditor` → read-only access

You can configure:

```bash
setfacl -m u:devops:rwx /app
setfacl -m u:developer:rwX /app
setfacl -m u:auditor:rX /app
```

Check:

```bash
getfacl /app
```

This allows different users to have different permissions **without changing the directory owner or primary group**.

---

## Quick Reference

```bash
getfacl file.txt                         # View ACL
setfacl -m u:john:rwx file.txt           # Give user permissions
setfacl -m u:john:rw file.txt            # Read + write
setfacl -m g:developers:rw file.txt      # Give group permissions
setfacl -x u:john file.txt               # Remove user ACL
setfacl -x g:developers file.txt         # Remove group ACL
setfacl -b file.txt                      # Remove all extended ACLs
setfacl -R -m u:john:rwx /project        # Recursive ACL
setfacl -d -m u:john:rwx /project        # Default ACL
getfacl -R /project > acl_backup.txt     # Backup ACL
setfacl --restore=acl_backup.txt         # Restore ACL
ls -l file.txt                           # Check for '+' indicator
```

> **Interview Point:** Linux standard permissions support **owner, group, and others**, while **ACL provides fine-grained permissions for specific users and groups** without changing the file's ownership.
