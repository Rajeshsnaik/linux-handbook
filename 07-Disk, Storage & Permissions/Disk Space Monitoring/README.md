# Linux Disk Space Monitoring

Disk space monitoring is the process of checking **available, used, and total storage** on a Linux system.

It is important for system administrators and DevOps engineers because a full disk can cause:

- Applications to stop working
- Databases to fail
- Logs to stop writing
- Servers to become unstable
- Deployments to fail

---

## `df` — Disk Free Space

The `df` command displays **filesystem-level disk usage**.

### Basic Command

```bash
df
```

### Human-Readable Format

```bash
df -h
```

Example:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       20G   12G  7.0G  64% /
```

Important columns:

| Column       | Description     |
| ------------ | --------------- |
| `Filesystem` | Disk/filesystem |
| `Size`       | Total size      |
| `Used`       | Used space      |
| `Avail`      | Available space |
| `Use%`       | Percentage used |
| `Mounted on` | Mount point     |

---

## Check Root Filesystem

```bash
df -h /
```

Useful when you specifically want to check the `/` filesystem.

---

## Check All Filesystems

```bash
df -h
```

Shows mounted filesystems such as:

```text
/
 /boot
 /home
 /var
```

depending on the system configuration.

---

## Check Inode Usage

Disk space can be available while **inodes are exhausted**.

Use:

```bash
df -i
```

Human-readable:

```bash
df -ih
```

Example:

```text
Filesystem      Inodes  IUsed   IFree IUse% Mounted on
/dev/xvda1        1.3M   200K    1.1M   16% /
```

> **Interview Point:** A filesystem can have free disk space but still fail to create files if it runs out of **inodes**.

---

# `du` — Disk Usage

The `du` command shows how much space is being used by **files and directories**.

### Check Current Directory

```bash
du -sh .
```

### Check a Specific Directory

```bash
du -sh /var
```

Example:

```text
4.5G    /var
```

---

## Find Large Directories

```bash
du -h --max-depth=1 /
```

Example:

```text
2.1G    /home
5.4G    /var
8.2G    /usr
16G     /
```

This helps identify which directories are consuming disk space.

---

## Find Largest Directories

```bash
du -h --max-depth=1 /var | sort -hr
```

This sorts directories from **largest to smallest**.

Example:

```text
5.2G    /var
3.8G    /var/log
1.2G    /var/lib
500M    /var/cache
```

---

## Find Large Files

You can use:

```bash
find /var -type f -size +500M -ls
```

This finds files larger than **500 MB**.

Another useful command:

```bash
find /var -type f -printf '%s %p\n' | sort -nr | head
```

This displays the largest files.

---

# Check Disk Usage with `lsblk`

`lsblk` displays information about **block devices and disks**.

```bash
lsblk
```

Example:

```text
NAME        SIZE TYPE MOUNTPOINT
xvda         20G disk
└─xvda1      20G part /
```

Human-readable:

```bash
lsblk -f
```

This also shows:

- Filesystem
- UUID
- Mount point
- Filesystem type

---

# Check Disk and Mount Points

```bash
df -hT
```

`-T` displays the filesystem type.

Example:

```text
Filesystem     Type  Size  Used Avail Use% Mounted on
/dev/xvda1     ext4   20G   12G  7.0G  64% /
```

---

# Monitor Disk Usage in Real Time

You can combine `watch` with `df`:

```bash
watch -n 5 df -h
```

This refreshes disk usage every **5 seconds**.

---

# Find Full Filesystems

A useful command:

```bash
df -h | awk 'NR==1 || $5+0 >= 80'
```

This displays filesystems where usage is **80% or higher**.

---

# Common Disk Monitoring Commands

```bash
df -h
df -hT
df -i
df -ih
du -sh .
du -sh /var
du -h --max-depth=1 /var
lsblk
lsblk -f
watch -n 5 df -h
```

---

# `df` vs `du`

| `df`                              | `du`                                       |
| --------------------------------- | ------------------------------------------ |
| Shows filesystem usage            | Shows file/directory usage                 |
| Shows total/used/free space       | Shows space used by files                  |
| Useful for checking disk capacity | Useful for finding what is consuming space |
| Works at filesystem level         | Works at directory/file level              |

### Example Troubleshooting

If:

```bash
df -h
```

shows:

```text
/dev/xvda1   20G   19G   1G   95% /
```

First identify large directories:

```bash
du -h --max-depth=1 / | sort -hr
```

Then investigate the largest directory:

```bash
du -h --max-depth=1 /var | sort -hr
```

Finally, find large files:

```bash
find /var -type f -size +500M -ls
```

This is a common Linux production troubleshooting workflow.

---

## Quick Reference

```bash
df -h                              # Check disk space
df -hT                             # Disk space + filesystem type
df -i                              # Check inode usage
df -ih                             # Human-readable inode usage

du -sh .                           # Current directory size
du -sh /var                        # Directory size
du -h --max-depth=1 /var           # Sizes of subdirectories
du -h --max-depth=1 /var | sort -hr # Sort by size

lsblk                              # List disks and partitions
lsblk -f                           # Disk + filesystem information

find /var -type f -size +500M -ls  # Find files > 500 MB

watch -n 5 df -h                   # Monitor disk usage
```

> **Interview Point:** Use `df -h` to check **filesystem-level disk usage**, and `du -sh` / `du` to identify **which files or directories are consuming the space**.
