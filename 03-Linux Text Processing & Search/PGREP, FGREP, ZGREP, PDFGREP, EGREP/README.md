# Linux PGREP, FGREP, ZGREP, PDFGREP, EGREP

## What is PGREP?

**`pgrep` (Process GREP)** is a Linux command used to search for **running processes** by their name or other attributes.

Unlike `grep`, which searches text, `pgrep` searches the **process table** and returns matching **Process IDs (PIDs)**.

### Syntax

```bash
pgrep [options] process_name
```

### Find Process by Name

```bash
pgrep nginx
```

This returns the PIDs of processes whose name matches `nginx`.

### Show Process Name with PID

Use **`-l`** to display the process name along with its PID:

```bash
pgrep -l ssh
```

Example:

```text
1234 sshd
2456 ssh-agent
```

### Match Full Command Line

Use **`-f`** to search the entire command line instead of only the process name:

```bash
pgrep -f "python app.py"
```

### Common Use Cases

- Find process IDs
- Check whether a process is running
- Find processes by name
- Use with `pkill` for process management
- Monitor background processes

---

## What is FGREP?

**`fgrep` (Fixed GREP)** searches for **literal strings** instead of regular expressions.

It is equivalent to:

```bash
grep -F
```

`grep -F` treats special regular-expression characters as ordinary characters.

> **Note:** `fgrep` is considered a legacy alias on modern systems. Prefer `grep -F`.

### Syntax

```bash
grep -F "text" file.txt
```

### Search a Literal String

```bash
grep -F "user.name" config.txt
```

Here, the `.` is treated as a literal dot rather than a regular-expression wildcard.

For example:

```text
user.name
```

will match exactly that text.

### Search Strings Containing Regex Characters

```bash
grep -F "price+$100" data.txt
```

Characters such as:

```text
.  +  *  ?  $  [  ]
```

are treated literally.

### Common Use Cases

- Search exact text
- Search strings containing regex characters
- Search configuration files
- Search large text files using fixed-string matching

---

## What is ZGREP?

**`zgrep`** searches for text inside **gzip-compressed `.gz` files** without requiring you to manually extract them first.

### Syntax

```bash
zgrep "pattern" file.gz
```

### Search a Compressed Log File

```bash
zgrep "ERROR" application.log.gz
```

### Ignore Case

```bash
zgrep -i "failed" server.log.gz
```

### Search Multiple Compressed Logs

```bash
zgrep "ERROR" *.log.gz
```

### Common Use Cases

- Search archived logs
- Analyze compressed server logs
- Troubleshoot historical production issues
- Search compressed backups

Example:

```text
/var/log/
    │
    ├── application.log
    ├── application.log.1
    ├── application.log.2.gz
    └── application.log.3.gz
```

Instead of extracting `application.log.2.gz`, you can directly run:

```bash
zgrep "ERROR" application.log.2.gz
```

---

## What is PDFGREP?

**`pdfgrep`** is a command-line utility used to search for text inside **PDF documents**.

> **Note:** `pdfgrep` is not installed by default on many Linux distributions.

### Syntax

```bash
pdfgrep "keyword" document.pdf
```

### Search a PDF

```bash
pdfgrep "Linux" handbook.pdf
```

### Show Line Numbers

```bash
pdfgrep -n "Docker" guide.pdf
```

### Ignore Case

```bash
pdfgrep -i "kubernetes" documentation.pdf
```

### Search Multiple PDF Files

```bash
pdfgrep "Linux" *.pdf
```

### Common Use Cases

- Search technical documentation
- Search Linux manuals
- Search ebooks
- Search PDF reports
- Find specific topics in documentation

---

## What is EGREP?

**`egrep` (Extended GREP)** was traditionally used to search using **Extended Regular Expressions (ERE)**.

It is equivalent to:

```bash
grep -E
```

Modern Linux systems generally recommend using **`grep -E`** instead of `egrep`.

### Syntax

```bash
grep -E "pattern" file.txt
```

### Search Multiple Keywords

```bash
grep -E "ERROR|WARNING|FAILED" logfile.txt
```

This matches lines containing:

```text
ERROR
WARNING
FAILED
```

### Match Numbers

```bash
grep -E "[0-9]+" data.txt
```

This searches for one or more digits.

### Match Multiple Extensions

```bash
grep -E "\.(log|txt|conf)$" files.txt
```

This matches filenames ending with:

```text
.log
.txt
.conf
```

### Common Use Cases

- Search multiple keywords
- Use extended regular expressions
- Analyze application logs
- Perform advanced text searches
- Filter command output

---

## Comparison

| Command             | Purpose                                   |
| ------------------- | ----------------------------------------- |
| `pgrep`             | Search running processes and return PIDs  |
| `grep -F` (`fgrep`) | Search fixed/literal strings              |
| `zgrep`             | Search inside `.gz` compressed files      |
| `pdfgrep`           | Search text inside PDF documents          |
| `grep -E` (`egrep`) | Search using extended regular expressions |

---

## grep Family at a Glance

```text
grep
 │
 ├── grep -F  → Fixed/literal string search
 │
 ├── grep -E  → Extended regular expressions
 │
 ├── zgrep    → Search compressed .gz files
 │
 ├── pdfgrep  → Search PDF documents
 │
 └── pgrep    → Search running processes
```

> **Important:** `pgrep`, `zgrep`, and `pdfgrep` are related by their search-oriented naming, but they are not simply different modes of the `grep` command. `pgrep` searches processes, `zgrep` works with gzip-compressed input, and `pdfgrep` is a separate utility for PDFs.

---

## When to Use Them

### `pgrep`

Use when you need to find running processes and their PIDs.

```bash
pgrep nginx
```

### `grep -F`

Use when you need to search for exact text containing special characters.

```bash
grep -F "user.name" config.txt
```

### `zgrep`

Use when you need to search compressed log files without extracting them.

```bash
zgrep "ERROR" application.log.gz
```

### `pdfgrep`

Use when you need to search text inside PDF documents.

```bash
pdfgrep "Linux" handbook.pdf
```

### `grep -E`

Use when you need extended regular expressions or multiple patterns.

```bash
grep -E "ERROR|WARNING|FAILED" logfile.txt
```

These commands are useful for **Linux administration, DevOps, SRE, log analysis, troubleshooting, process management, shell scripting, and system operations**.
