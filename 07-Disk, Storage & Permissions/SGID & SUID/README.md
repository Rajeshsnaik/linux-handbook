# Linux SUID and SGID — Special Permissions

**SUID** and **SGID** are special Linux permissions that control how a file or directory behaves when it is executed or accessed.

They are useful when a program needs to temporarily operate with the permissions of its **owner** or **group**.

Linux has three special permission bits:

- **SUID** → Set User ID
- **SGID** → Set Group ID
- **Sticky Bit** → Restricts deletion in shared directories

This document focuses on **SUID and SGID**.

---

# SUID — Set User ID

**SUID** stands for **Set User ID**.

When SUID is set on an **executable file**, the program runs with the permissions of the **file owner**, rather than the user who executed it.

### Example

Suppose:

```text
Owner → root
File  → /usr/bin/example
```

If SUID is enabled and a normal user runs the program:

```bash
./example
```

the program can run with the **effective user ID of the owner**.

If the owner is `root`:

```text
Normal User
     ↓
Runs program
     ↓
SUID enabled
     ↓
Effective UID = root
```

> **Security Note:** SUID programs must be carefully controlled because a vulnerable SUID-root program can potentially allow privilege escalation.

---

# Check SUID

Use:

```bash
ls -l /path/to/file
```

Example:

```text
-rwsr-xr-x 1 root root 12345 Aug 21 example
```

Notice:

```text
-rwsr-xr-x
   ^
   s
```

The `s` in the **owner execute position** indicates SUID.

Normal:

```text
-rwxr-xr-x
```

SUID:

```text
-rwsr-xr-x
```

---

# Set SUID

Using symbolic notation:

```bash
chmod u+s file
```

Example:

```bash
chmod u+s example
```

Using numeric notation:

```bash
chmod 4755 example
```

Here:

```text
4 → SUID
7 → Owner permissions
5 → Group permissions
5 → Others permissions
```

---

# Remove SUID

```bash
chmod u-s example
```

Or:

```bash
chmod 0755 example
```

---

# Find SUID Files

To find SUID files on the system:

```bash
find / -perm -4000 -type f 2>/dev/null
```

This is useful during **Linux security audits**.

---

# SGID — Set Group ID

**SGID** stands for **Set Group ID**.

SGID behaves differently depending on whether it is applied to a **file** or a **directory**.

---

# SGID on Executable Files

When SGID is set on an executable file, the program runs with the **effective group ID of the file's group**.

Example:

```text
File owner → root
File group → developers
```

With SGID:

```text
User
 ↓
Runs program
 ↓
SGID enabled
 ↓
Effective GID = developers
```

Check:

```bash
ls -l example
```

Example:

```text
-rwxr-sr-x 1 root developers 12345 Aug 21 example
```

Notice the:

```text
s
```

in the **group execute position**.

---

# SGID on Directories

SGID is especially useful on **shared directories**.

When SGID is enabled on a directory:

> New files and subdirectories created inside it inherit the directory's **group ownership**.

Example:

```text
/project
Group → developers
```

Set SGID:

```bash
chmod g+s /project
```

Now:

```text
/project
    ↓
New file created
    ↓
Group → developers
```

This is very useful for **shared development directories**.

---

# Check SGID on a Directory

```bash
ls -ld /project
```

Example:

```text
drwxrwsr-x 2 root developers 4096 Aug 21 /project
```

Notice:

```text
     ^
     s
```

The `s` appears in the **group execute position**.

---

# Set SGID

### On a File

```bash
chmod g+s file
```

### On a Directory

```bash
chmod g+s /project
```

Numeric notation:

```bash
chmod 2775 /project
```

Here:

```text
2 → SGID
7 → Owner permissions
7 → Group permissions
5 → Others permissions
```

---

# Remove SGID

Symbolic:

```bash
chmod g-s /project
```

Numeric example:

```bash
chmod 0755 /project
```

---

# Find SGID Files

```bash
find / -perm -2000 -type f 2>/dev/null
```

Find SGID directories:

```bash
find / -perm -2000 -type d 2>/dev/null
```

---

# SUID vs SGID

| SUID                                             | SGID                                                         |
| ------------------------------------------------ | ------------------------------------------------------------ |
| Set User ID                                      | Set Group ID                                                 |
| Mainly used on executable files                  | Used on executable files and directories                     |
| Runs with file owner's effective UID             | Executable runs with file group's effective GID              |
| Directory behavior is generally not the main use | Directory SGID makes new files inherit the directory's group |
| Numeric value: `4`                               | Numeric value: `2`                                           |

---

# SUID and SGID Permissions

Linux special permission values:

```text
SUID → 4
SGID → 2
Sticky Bit → 1
```

They are placed before the normal three permission digits.

Example:

```bash
chmod 4755 file
```

Means:

```text
SUID + 755
```

Example:

```bash
chmod 2775 /project
```

Means:

```text
SGID + 775
```

---

# SUID + SGID Together

You can set both SUID and SGID:

```bash
chmod 6755 example
```

Breakdown:

```text
6 → SUID + SGID
7 → Owner
5 → Group
5 → Others
```

Because:

```text
4 + 2 = 6
```

Check:

```bash
ls -l example
```

You may see:

```text
-rwsr-sr-x
```

Here:

```text
s → SUID
s → SGID
```

---

# Understanding `s` and `S`

You may see either lowercase `s` or uppercase `S`.

### Lowercase `s`

```text
-rwsr-xr-x
```

The special permission and execute permission are both set.

### Uppercase `S`

```text
-rwSr--r--
```

The special permission is set, but the corresponding execute permission is **not** set.

For example:

```bash
chmod 4644 file
```

may produce an uppercase `S` because the owner execute bit is not set.

---

# Real-World SGID Example

Suppose a development team uses:

```text
/opt/project
```

The directory belongs to:

```text
root:developers
```

Set the correct group:

```bash
chgrp developers /opt/project
```

Give the group appropriate permissions:

```bash
chmod 2775 /opt/project
```

Now SGID is enabled.

When a developer creates:

```bash
touch /opt/project/app.log
```

the file inherits the directory's group:

```text
root:developers
```

instead of necessarily inheriting the creator's primary group.

This makes **shared project directories** much easier to manage.

---

# SUID Security Example

Find SUID files:

```bash
find / -perm -4000 -type f 2>/dev/null
```

You may find programs such as:

```text
/usr/bin/passwd
```

A password-changing program needs to perform operations involving protected system files.

SUID allows the program to execute with the appropriate owner privileges.

> **Security Best Practice:** Avoid adding SUID unnecessarily, especially SUID-root. Regularly audit SUID/SGID files and remove special permissions that are not required.

---

# SUID vs Normal Permissions

Without SUID:

```text
User
 ↓
Runs program
 ↓
Program uses user's effective UID
```

With SUID:

```text
User
 ↓
Runs program
 ↓
SUID
 ↓
Program uses file owner's effective UID
```

---

# SGID Directory Behavior

Without SGID:

```text
/project
Group → developers

User creates file
      ↓
File group may be user's default group
```

With SGID:

```text
/project
Group → developers
SGID enabled
      ↓
User creates file
      ↓
File inherits developers group
```

---

# Quick Reference

```bash
# SUID
chmod u+s file                    # Set SUID
chmod u-s file                    # Remove SUID
chmod 4755 file                   # Set SUID + 755

# SGID
chmod g+s file                    # Set SGID
chmod g-s file                    # Remove SGID
chmod 2775 directory              # Set SGID + 775

# SUID + SGID
chmod 6755 file                   # Set both

# Find SUID
find / -perm -4000 -type f 2>/dev/null

# Find SGID
find / -perm -2000 -type f 2>/dev/null

# Check permissions
ls -l file
ls -ld directory
```

---

> **Interview Points:**
>
> - **SUID (`4`)** → Executable runs with the **file owner's effective UID**.
> - **SGID (`2`)** → Executable runs with the **file group's effective GID**.
> - **SGID on a directory** → New files/directories inherit the directory's **group**.
> - `s` means the special bit and execute permission are both set.
> - `S` means the special bit is set but execute permission is not.
> - SUID/SGID should be carefully managed because incorrect use can create **security risks**.
