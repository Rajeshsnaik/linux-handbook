# Linux Hard & Soft Links | `ln` Command

## What are Links in Linux?

A **link** allows multiple filenames to reference the same file data or provides a shortcut to another file or directory.

Linux has two main types:

- **Hard Link**
- **Soft Link (Symbolic Link)**

---

# `ln` Command

The `ln` command creates links.

### Hard Link

```bash
ln file.txt hardlink.txt
```

### Soft Link

```bash
ln -s file.txt softlink.txt
```

---

# Hard Link

A **hard link** is another filename pointing to the **same inode and data** as the original file.

```text
file.txt
    │
    ├── Same Inode
    │
hardlink.txt
```

Create:

```bash
ln file.txt hardlink.txt
```

Check inode numbers:

```bash
ls -li
```

Both files will have the **same inode number**.

### Characteristics

- Same inode as the original file.
- Data remains if the original filename is deleted.
- Cannot normally link directories.
- Cannot cross different filesystems.

---

# Soft Link (Symbolic Link)

A **soft link** is a special file that points to the **path** of another file or directory.

```text
softlink.txt
      │
      ▼
  file.txt
      │
      ▼
  File Data
```

Create:

```bash
ln -s file.txt softlink.txt
```

Check:

```bash
ls -l
```

Example:

```text
softlink.txt -> file.txt
```

### Characteristics

- Has its own inode.
- Stores the target path.
- Can link to files and directories.
- Can cross different filesystems.
- Becomes a **broken link** if the target is deleted.

---

# Hard Link vs Soft Link

| Hard Link                             | Soft Link                   |
| ------------------------------------- | --------------------------- |
| `ln file link`                        | `ln -s file link`           |
| Same inode                            | Different inode             |
| Points to file data                   | Points to file path         |
| Works if original filename is deleted | Breaks if target is deleted |
| Cannot normally link directories      | Can link directories        |
| Cannot cross filesystems              | Can cross filesystems       |

---

# Check Inodes

```bash
ls -li
```

Example:

```text
12345 -rw-r--r-- file.txt
12345 -rw-r--r-- hardlink.txt
67890 lrwxrwxrwx softlink.txt -> file.txt
```

Here:

- `file.txt` and `hardlink.txt` → same inode
- `softlink.txt` → different inode

---

# Remove Links

```bash
rm hardlink.txt
rm softlink.txt
```

Removing a link does not affect the original file.

---

# Common Use Cases

### Configuration Link

```bash
ln -s /etc/nginx/nginx.conf nginx.conf
```

### Application Directory

```bash
ln -s /var/www/html website
```

### Multiple Names for Same Data

```bash
ln report.txt report_backup.txt
```

---

# Best Practices

- Use **soft links** for shortcuts and directories.
- Use **hard links** when multiple filenames should reference the same data.
- Use `ls -li` to check inode numbers.
- Check symbolic links before deleting or moving their targets.
- Use symbolic links commonly for application versions, configurations, and shared directories.

---

## Why Learn Links?

Understanding hard and soft links is important for **Linux administration, DevOps, deployments, configuration management, and troubleshooting**. The `ln` command helps manage files efficiently without unnecessary duplication.
