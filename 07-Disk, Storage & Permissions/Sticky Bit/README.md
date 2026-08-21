# Sticky Bit — Restricted Deletion Flag

The **Sticky Bit** is a special Linux permission used mainly on **shared directories**.

When the Sticky Bit is enabled on a directory:

> Users can create files in the directory, but they can normally delete or rename **only files they own**.

This prevents one user from deleting another user's files in a shared directory.

---

## Why Use Sticky Bit?

Consider a shared directory:

```text
/shared
```

Suppose:

```text
rajesh   → file1.txt
john     → file2.txt
```

Both users have write permission on `/shared`.

Without Sticky Bit:

```text
john
 ↓
Can potentially delete
 ↓
rajesh's file1.txt
```

With Sticky Bit:

```text
john
 ↓
Can delete
 ↓
Only files he is allowed to delete
```

This is why Sticky Bit is commonly used on directories such as:

```text
/tmp
```

---

# Check Sticky Bit

Use:

```bash
ls -ld /tmp
```

Example:

```text
drwxrwxrwt 12 root root 4096 Aug 21 /tmp
```

Notice the:

```text
t
```

at the end:

```text
drwxrwxrwt
         ^
         t
```

The `t` indicates that the **Sticky Bit is enabled**.

---

# Normal Directory vs Sticky Bit

### Without Sticky Bit

```text
drwxrwxrwx
```

### With Sticky Bit

```text
drwxrwxrwt
```

The final:

```text
t
```

represents the Sticky Bit.

---

# Set Sticky Bit

### Symbolic Method

```bash
chmod +t /shared
```

Example:

```bash
mkdir /shared
chmod 1777 /shared
```

Now check:

```bash
ls -ld /shared
```

You should see:

```text
drwxrwxrwt
```

---

# Numeric Method

The Sticky Bit has the special permission value:

```text
1
```

Example:

```bash
chmod 1777 /shared
```

Breakdown:

```text
1 → Sticky Bit
7 → Owner: rwx
7 → Group: rwx
7 → Others: rwx
```

Therefore:

```text
1777 = Sticky Bit + rwxrwxrwx
```

---

# Remove Sticky Bit

Using symbolic notation:

```bash
chmod -t /shared
```

Or using numeric permissions:

```bash
chmod 0777 /shared
```

---

# `t` vs `T`

You may see either lowercase `t` or uppercase `T`.

### Lowercase `t`

```text
drwxrwxrwt
```

Means:

- Sticky Bit is enabled
- Others also have execute permission

### Uppercase `T`

```text
drwxrwxrwT
```

Means:

- Sticky Bit is enabled
- Others do **not** have execute permission

---

# Real-World Example

Create a shared directory:

```bash
mkdir /shared
```

Give everyone read/write/execute permission:

```bash
chmod 777 /shared
```

Now enable Sticky Bit:

```bash
chmod +t /shared
```

Or directly:

```bash
chmod 1777 /shared
```

Check:

```bash
ls -ld /shared
```

Output:

```text
drwxrwxrwt 2 root root 4096 Aug 21 /shared
```

Now users can work in the shared directory, while the Sticky Bit helps prevent users from deleting or renaming files belonging to other users.

---

# `/tmp` — Common Example

The `/tmp` directory is a classic example:

```bash
ls -ld /tmp
```

Typical output:

```text
drwxrwxrwt 20 root root 4096 Aug 21 /tmp
```

It is:

```text
Owner  → rwx
Group  → rwx
Others → rwx
Sticky → enabled
```

This allows multiple users and applications to use `/tmp` while restricting deletion/renaming of files owned by other users.

---

# Sticky Bit Deletion Rules

For a directory with Sticky Bit enabled, deletion or renaming is generally restricted to:

- The **file owner**
- The **directory owner**
- **root** / a sufficiently privileged process

Example:

```text
/shared
├── rajesh.txt    → owned by rajesh
└── john.txt      → owned by john
```

If both users can write to `/shared` and Sticky Bit is enabled:

```text
rajesh → can delete rajesh.txt
rajesh → cannot normally delete john.txt

john   → can delete john.txt
john   → cannot normally delete rajesh.txt
```

> **Important:** Sticky Bit controls deletion/rename within the directory. It does not prevent users from modifying a file if they already have write permission on that file.

---

# Sticky Bit vs `chmod 777`

A common mistake is to think:

```bash
chmod 777 /shared
```

is enough for a shared directory.

`777` allows everyone to write to the directory, but without Sticky Bit, users may be able to remove or rename files belonging to other users.

A safer shared-directory pattern is:

```bash
chmod 1777 /shared
```

This means:

```text
777  → Everyone can access/write
1    → Sticky Bit restricts deletion/rename
```

---

# Sticky Bit vs SGID

Both are commonly used with shared directories, but they solve different problems.

| Sticky Bit                                  | SGID                                |
| ------------------------------------------- | ----------------------------------- |
| Restricts deletion/rename                   | Controls group inheritance          |
| Protects users' files in shared directories | New files inherit directory's group |
| Permission value: `1`                       | Permission value: `2`               |
| Example: `/tmp`                             | Example: `/project`                 |

They can also be used together.

Example:

```bash
chmod 3775 /shared
```

Breakdown:

```text
3 → SGID + Sticky Bit
7 → Owner
7 → Group
5 → Others
```

---

# Special Permission Values

Linux has three commonly discussed special permission bits:

```text
SUID       → 4
SGID       → 2
Sticky Bit → 1
```

Examples:

```text
4755 → SUID + 755
2775 → SGID + 775
1777 → Sticky Bit + 777
3775 → SGID + Sticky Bit + 775
```

---

# Find Sticky Bit Directories

You can search for directories with Sticky Bit enabled:

```bash
find / -type d -perm -1000 2>/dev/null
```

This can be useful during Linux security audits.

---

# Important Points

- Sticky Bit is mainly used on **shared directories**.
- It restricts who can **delete or rename** files inside the directory.
- The permission value is **`1`**.
- Lowercase `t` means Sticky Bit + execute permission.
- Uppercase `T` means Sticky Bit without execute permission.
- `/tmp` is the most common real-world example.
- Sticky Bit does **not** control whether a user can read or modify a file.
- For shared project directories, **SGID** is often used together with appropriate group permissions.

---

# Quick Reference

```bash
# Check Sticky Bit
ls -ld /tmp

# Set Sticky Bit
chmod +t /shared

# Set Sticky Bit using numeric mode
chmod 1777 /shared

# Remove Sticky Bit
chmod -t /shared

# Find Sticky Bit directories
find / -type d -perm -1000 2>/dev/null
```

### Permission Representation

```text
drwxrwxrwt
         ↑
     Sticky Bit
```

### Numeric Representation

```text
1777
│
└── Sticky Bit
```

> **Interview Point:** The **Sticky Bit** is mainly used on shared directories such as `/tmp`. It allows users to create files while restricting them from deleting or renaming files owned by other users. The numeric value of the Sticky Bit is **`1`**.
