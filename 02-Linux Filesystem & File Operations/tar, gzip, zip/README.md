# Linux Compression: `tar`, `gzip`, and `zip`

## What is File Compression?

Compression reduces file size, while archiving combines multiple files into a single archive.

Common Linux tools:

- `tar` → Archive files/directories
- `gzip` → Compress files
- `zip` → Archive and compress files

---

# `tar` Command

`tar` creates an archive but **does not compress by itself**.

### Create Archive

```bash
tar -cvf backup.tar project/
```

- `c` → Create
- `v` → Verbose
- `f` → Filename

### View Contents

```bash
tar -tvf backup.tar
```

### Extract Archive

```bash
tar -xvf backup.tar
```

### Extract to Specific Directory

```bash
tar -xvf backup.tar -C /backup/
```

---

# `gzip` Command

`gzip` compresses a file and creates a `.gz` file.

### Compress

```bash
gzip logfile.log
```

Creates:

```text
logfile.log.gz
```

### Decompress

```bash
gunzip logfile.log.gz
```

or:

```bash
gzip -d logfile.log.gz
```

### Keep Original File

```bash
gzip -k report.txt
```

---

# `tar` + `gzip`

`tar` and `gzip` are commonly combined to create `.tar.gz` archives.

### Create `.tar.gz`

```bash
tar -czvf backup.tar.gz project/
```

- `c` → Create
- `z` → gzip compression
- `v` → Verbose
- `f` → Filename

### Extract

```bash
tar -xzvf backup.tar.gz
```

### Extract to Specific Directory

```bash
tar -xzvf backup.tar.gz -C /backup/
```

---

# `zip` Command

`zip` creates compressed `.zip` archives and is widely supported across **Linux, Windows, and macOS**.

### Create ZIP

```bash
zip documents.zip file1.txt file2.txt
```

### Compress Directory

```bash
zip -r project.zip project/
```

### View Contents

```bash
unzip -l project.zip
```

### Extract

```bash
unzip project.zip
```

### Extract to Specific Directory

```bash
unzip project.zip -d /backup/
```

---

# TAR vs GZIP vs ZIP

| Tool         | Purpose                   | Output    |
| ------------ | ------------------------- | --------- |
| `tar`        | Archive files/directories | `.tar`    |
| `gzip`       | Compress a file           | `.gz`     |
| `tar + gzip` | Archive + compress        | `.tar.gz` |
| `zip`        | Archive + compress        | `.zip`    |

---

# Common Use Cases

### Backup Application

```bash
tar -czvf backup.tar.gz /var/www
```

### Compress Logs

```bash
gzip access.log
```

### Share Files Across Operating Systems

```bash
zip -r website.zip website/
```

### Extract Backup

```bash
tar -xzvf website_backup.tar.gz
```

---

# Best Practices

- Use **`tar`** to archive Linux files and directories.
- Use **`gzip`** for individual file compression.
- Use **`.tar.gz`** for Linux backups and deployments.
- Use **`zip`** for cross-platform file sharing.
- Check archive contents before extracting.
- Extract archives carefully to avoid overwriting files.

---

## Why Learn Compression Commands?

`tar`, `gzip`, and `zip` are essential for **Linux administration, backups, log management, deployments, and file transfers**. They help reduce storage usage and make file management easier.
