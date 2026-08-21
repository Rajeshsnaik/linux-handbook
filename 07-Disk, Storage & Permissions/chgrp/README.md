# `chgrp` — Change Group Ownership

`chgrp` stands for **Change Group**.

It is used to change the **group ownership** of files and directories in Linux.

Every file and directory in Linux has:

- **Owner (User)**
- **Group**
- **Others**

`chgrp` changes **only the group**. It does not change the file's owner.

---

## Basic Command

```bash
chgrp <group> <file>
```

Example:

```bash
chgrp developers file.txt
```

This changes the group of `file.txt` to:

```text
developers
```

---

## Check Group Ownership

Use:

```bash
ls -l file.txt
```

Example:

```text
-rw-r--r-- 1 rajesh developers 1024 Aug 21 file.txt
```

Here:

```text
rajesh      → Owner
developers  → Group
```

---

# Change Group of a Directory

```bash
chgrp developers project/
```

This changes the group of the directory itself.

Check:

```bash
ls -ld project/
```

---

# Recursive Group Change

To change the group of a directory and **everything inside it**:

```bash
chgrp -R developers project/
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
chgrp -R developers project/
```

changes the group of:

```text
project/
app.js
config/
app.conf
logs/
app.log
```

---

# Verbose Mode

Use `-v` to display the changes:

```bash
chgrp -v developers file.txt
```

Example output:

```text
changed group of 'file.txt' from users to developers
```

---

# Check Before Changing

You can check the current ownership using:

```bash
ls -l file.txt
```

Or:

```bash
stat file.txt
```

Example:

```text
Uid: (1001/rajesh)
Gid: (1002/users)
```

After:

```bash
chgrp developers file.txt
```

The group becomes:

```text
Gid: (1003/developers)
```

---

# Using `sudo`

If you don't have permission to change the group:

```bash
sudo chgrp developers file.txt
```

For a directory:

```bash
sudo chgrp -R developers /opt/project
```

---

# Change Group Using GID

You can also specify the numeric **GID**:

```bash
chgrp 1002 file.txt
```

Check the result:

```bash
ls -ln file.txt
```

The `-n` option displays numeric UID/GID values.

---

# `chgrp` with Symbolic Links

For symbolic links, `-h` can be used to change the group of the **link itself** rather than the target:

```bash
chgrp -h developers app.log
```

---

# Change Group Based on Another File

You can use `--reference` to copy the group ownership from another file:

```bash
chgrp --reference=file1.txt file2.txt
```

Now `file2.txt` gets the same group as `file1.txt`.

---

# Real-World Example

Suppose multiple developers work on:

```text
/opt/project
```

The directory currently belongs to:

```text
root:root
```

You have a group:

```text
developers
```

Change the group:

```bash
sudo chgrp -R developers /opt/project
```

Now the files can belong to:

```text
root:developers
```

The owner remains:

```text
root
```

Only the group changes.

---

# `chgrp` vs `chown`

| `chgrp`                  | `chown`                        |
| ------------------------ | ------------------------------ |
| Changes only group       | Changes owner and/or group     |
| `chgrp developers file`  | `chown rajesh:developers file` |
| Owner remains unchanged  | Owner can be changed           |
| Simpler group management | Complete ownership management  |

Example:

```bash
chgrp developers file.txt
```

Changes:

```text
Owner → unchanged
Group → developers
```

Whereas:

```bash
chown rajesh:developers file.txt
```

can change:

```text
Owner → rajesh
Group → developers
```

---

# `chgrp` vs `chmod`

These commands have different purposes.

### `chgrp`

Changes **group ownership**:

```bash
chgrp developers file.txt
```

### `chmod`

Changes **permissions**:

```bash
chmod 770 file.txt
```

Example:

```bash
chgrp developers project/
chmod 770 project/
```

Result:

```text
Owner  → full access
Group  → full access
Others → no access
```

---

# Important Points

- `chgrp` means **Change Group**.
- It changes only the **group ownership**.
- It does not change the file owner.
- `-R` changes the group recursively.
- `sudo` may be required.
- `ls -l` and `stat` can verify group ownership.
- `chown` can also change groups, but `chgrp` is specifically designed for group ownership.

---

# Quick Reference

```bash
chgrp developers file.txt                 # Change group
chgrp developers directory/               # Change directory group
chgrp -R developers directory/            # Recursive group change
chgrp -v developers file.txt              # Verbose output
chgrp 1002 file.txt                       # Change using GID
chgrp -h developers symlink                # Change symlink group
chgrp --reference=file1.txt file2.txt     # Copy group ownership
ls -l file.txt                            # Check ownership
stat file.txt                             # Detailed ownership
```

> **Interview Point:** `chgrp` changes the **group ownership** of a file or directory without changing its owner. `chown` can change the **owner and/or group**, while `chmod` changes the **permissions**.
