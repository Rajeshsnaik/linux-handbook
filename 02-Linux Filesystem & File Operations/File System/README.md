# Linux File System

## What is the Linux File System?

The **Linux File System** is a hierarchical structure used to organize files and directories. Everything starts from the **root directory `/`**.

---

## Linux File System Hierarchy

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

---

## Root Directory `/`

The `/` directory is the **top-level directory**. All files and directories exist under it.

---

## `/bin` — Essential Commands

Contains essential commands used by users.

Examples:

```text
ls
cp
mv
cat
rm
mkdir
```

---

## `/boot` — Boot Files

Contains files required to start Linux.

Examples:

```text
Linux Kernel
initramfs
GRUB
```

---

## `/dev` — Device Files

Contains files representing hardware and virtual devices.

Examples:

```text
/dev/sda
/dev/null
/dev/tty
/dev/random
```

---

## `/etc` — Configuration Files

Contains system-wide configuration files.

Important files:

```text
/etc/passwd
/etc/shadow
/etc/group
/etc/hosts
/etc/hostname
/etc/fstab
/etc/ssh/sshd_config
```

This is one of the **most important directories for Linux administration and DevOps**.

---

## `/home` — User Home Directories

Contains personal directories of regular users.

Example:

```text
/home/ubuntu
/home/rajesh
```

Used for storing user files, applications, and personal data.

---

## `/lib` — Shared Libraries

Contains shared libraries required by system programs and commands.

---

## `/media` — Removable Devices

Used for removable storage such as:

- USB drives
- DVDs
- External drives

---

## `/mnt` — Temporary Mount Point

Used to manually mount filesystems temporarily.

Example:

```bash
sudo mount /dev/sdb1 /mnt
```

---

## `/opt` — Optional Software

Used for optional or third-party applications.

Example:

```text
/opt/myapp
/opt/software
```

---

## `/proc` — Process Information

A virtual filesystem containing information about running processes and the kernel.

Examples:

```text
/proc/cpuinfo
/proc/meminfo
/proc/version
```

Useful for **system monitoring and troubleshooting**.

---

## `/root` — Root User Home

Home directory of the **root user**.

```text
/root
```

> `/root` is different from `/`.

---

## `/run` — Runtime Data

Contains temporary runtime information such as:

- Process IDs
- Socket files
- Service information

---

## `/sbin` — System Administration Commands

Contains commands mainly used for system administration.

Examples:

```text
fdisk
mount
reboot
shutdown
```

---

## `/srv` — Service Data

Contains data provided by system services.

Examples:

```text
Web server data
FTP data
```

---

## `/sys` — System Information

A virtual filesystem that provides information about:

- Hardware
- Devices
- Drivers
- Linux kernel

---

## `/tmp` — Temporary Files

Used for temporary files created by applications and users.

```text
/tmp
```

Temporary files may be removed automatically.

---

## `/usr` — User Programs

Contains applications, libraries, and documentation.

Important directories:

```text
/usr/bin
/usr/lib
/usr/share
/usr/local
```

---

## `/var` — Variable Data

Contains data that frequently changes.

Important locations:

```text
/var/log      → System and application logs
/var/cache    → Cached data
/var/lib      → Application data
```

`/var/log` is especially important for **troubleshooting Linux servers**.

---

# Important Linux Files

| File                   | Purpose                                 |
| ---------------------- | --------------------------------------- |
| `/etc/passwd`          | User account information                |
| `/etc/shadow`          | Password and password-aging information |
| `/etc/group`           | Group information                       |
| `/etc/hosts`           | Local hostname-to-IP mapping            |
| `/etc/hostname`        | System hostname                         |
| `/etc/fstab`           | Filesystem mount configuration          |
| `/etc/ssh/sshd_config` | SSH server configuration                |
| `/var/log/`            | System and application logs             |
| `/proc/cpuinfo`        | CPU information                         |
| `/proc/meminfo`        | Memory information                      |

---

# Important File System Commands

### Show Current Directory

```bash
pwd
```

### List Files

```bash
ls
```

### Change Directory

```bash
cd /etc
```

### Check Disk Usage

```bash
df -h
```

### Check Directory Size

```bash
du -sh /var/log
```

### Show Mounted Filesystems

```bash
mount
```

---

# Common Use Cases

- Navigate Linux directories
- Find configuration files
- Manage user files
- Troubleshoot logs
- Mount storage
- Install applications
- Analyze disk usage
- Monitor system resources

---

# Best Practices

- Store personal files under `/home`.
- Avoid modifying `/etc` without understanding the configuration.
- Check `/var/log` when troubleshooting.
- Use `/tmp` for temporary data.
- Use `/opt` for appropriate third-party applications.
- Monitor disk usage with `df` and `du`.

---

# Why Learn the Linux File System?

Understanding the Linux filesystem is essential for **Linux administration, DevOps, cloud computing, and troubleshooting**.

Knowing where **configuration files, logs, applications, user data, and system information** are stored helps you manage and troubleshoot Linux servers efficiently.
