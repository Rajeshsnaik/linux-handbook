# Linux `find` Command

## What is `find`?

The **`find`** command searches for files and directories based on conditions such as **name, type, size, owner, permissions, time, and inode**.

### Syntax

```bash
find <path> [options] [expression]
```

Example:

```bash
find /home -name "file.txt"
```

---

## Search by Name

```bash
find . -name "data.txt"
find . -name "*.log"
```

Case-insensitive:

```bash
find . -iname "readme.txt"
```

---

## Search by Type

Files only:

```bash
find . -type f
```

Directories only:

```bash
find . -type d
```

---

## Search by Size

Larger than 100 MB:

```bash
find . -size +100M
```

Smaller than 10 MB:

```bash
find . -size -10M
```

Between 1 MB and 50 MB:

```bash
find . -size +1M -size -50M
```

---

## Search by Owner

```bash
find /home -user ubuntu
```

---

## Search by Permissions

Find files with `755` permission:

```bash
find . -perm 755
```

Find writable files:

```bash
find . -perm -222
```

---

## Search by Modification Time

Exactly 15 days old:

```bash
find . -mtime 15
```

Older than 15 days:

```bash
find . -mtime +15
```

Modified within the last 15 days:

```bash
find . -mtime -15
```

---

## Search by Inode

```bash
find . -inum 123456
```

Useful when you know the inode number.

---

## Search by Hard Link Count

```bash
find . -links 2
```

Finds files with exactly two hard links.

---

## Find Newer Files

Find files modified after another file:

```bash
find . -newer last.txt
```

---

## Find Empty Files

```bash
find . -type f -empty
```

Find empty directories:

```bash
find . -type d -empty
```

---

## Delete Matching Files

Delete empty files:

```bash
find . -type f -empty -delete
```

> ⚠️ Be careful with `-delete`. Always verify the results before deleting files.

---

## Common Options

| Option    | Purpose                            |
| --------- | ---------------------------------- |
| `-name`   | Search by name                     |
| `-iname`  | Case-insensitive name search       |
| `-type f` | Files only                         |
| `-type d` | Directories only                   |
| `-size`   | Search by size                     |
| `-user`   | Search by owner                    |
| `-perm`   | Search by permissions              |
| `-mtime`  | Search by modification time        |
| `-newer`  | Find files newer than another file |
| `-empty`  | Find empty files/directories       |
| `-inum`   | Search by inode                    |
| `-links`  | Search by hard-link count          |
| `-delete` | Delete matching files              |

---

## Common Use Cases

- Find log files
- Locate large files
- Find old backups
- Search configuration files
- Find files by owner or permissions
- Clean up unused files
- Find recently modified files
- Troubleshoot disk-space issues

---

## Why Learn `find`?

`find` is an essential Linux administration command used for **file management, cleanup, log analysis, backups, troubleshooting, and automation**.

It becomes even more powerful when combined with **`grep`**, **`xargs`**, and **`-exec`**.
