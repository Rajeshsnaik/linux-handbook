## What is GREP?

**`grep` (Global Regular Expression Print)** is a Linux command used to search for text, keywords, and patterns inside files or command output.

It is one of the most commonly used commands by **Linux administrators, DevOps engineers, developers, and SREs** for:

- Log analysis
- Troubleshooting
- Searching configuration files
- Finding errors and warnings
- Filtering command output
- Searching source code

---

## GREP Syntax

```bash
grep [options] "pattern" file
```

Example:

```bash
grep "ERROR" logfile.txt
```

This searches `logfile.txt` for lines containing `ERROR`.

---

## Case 1: Ignore Upper and Lower Case

Use the **`-i`** option for a case-insensitive search.

```bash
grep -i "linux" file.txt
```

This matches:

```text
Linux
LINUX
linux
LiNuX
```

---

## Case 2: Search Everything Except a Pattern

Use **`-v`** to invert the match.

```bash
grep -v "error" logfile.txt
```

This displays all lines that **do not contain** `error`.

---

## Case 3: Count Matching Lines

Use **`-c`** to count the number of matching lines.

```bash
grep -c "ERROR" logfile.txt
```

Example output:

```text
15
```

This means 15 lines contain `ERROR`.

> `-c` counts matching **lines**, not necessarily every occurrence of the word.

---

## Case 4: Search for an Exact Word

Use **`-w`** to match a complete word.

```bash
grep -w "cat" file.txt
```

This matches:

```text
cat
```

But does not match:

```text
category
catalog
concatenate
```

---

## Case 5: Print Line Numbers

Use **`-n`** to display the line number of each matching line.

```bash
grep -n "ERROR" logfile.txt
```

Example output:

```text
25:ERROR Database connection failed
48:ERROR Authentication failed
```

---

## Case 6: Search Multiple Files

Specify multiple filenames:

```bash
grep "ERROR" file1.txt file2.txt file3.txt
```

GREP searches all three files.

Example:

```bash
grep "ERROR" app.log nginx.log system.log
```

---

## Case 7: Suppress File Names

When searching multiple files, GREP normally displays the filename.

Use **`-h`** to hide filenames.

```bash
grep -h "ERROR" *.log
```

This displays only the matching lines.

---

## Case 8: Search Multiple Keywords in One File

Use **`-e`** to specify multiple patterns.

```bash
grep -e "ERROR" -e "WARNING" logfile.txt
```

This matches lines containing either:

```text
ERROR
WARNING
```

---

## Case 9: Search Multiple Keywords in Multiple Files

```bash
grep -e "ERROR" -e "WARNING" *.log
```

This searches all `.log` files for both `ERROR` and `WARNING`.

---

## Case 10: Print Only Matching File Names

Use **`-l`** to display only the names of files containing the pattern.

```bash
grep -l "ERROR" *.log
```

Example output:

```text
app.log
server.log
database.log
```

---

## Case 11: Match Patterns from Another File

Use **`-f`** to read search patterns from a file.

Suppose `patterns.txt` contains:

```text
ERROR
WARNING
FAILED
```

Run:

```bash
grep -f patterns.txt logfile.txt
```

GREP searches for all patterns listed in `patterns.txt`.

---

## Case 12: Match Lines Starting with a Keyword

Use the **`^`** regular expression anchor.

```bash
grep "^ERROR" logfile.txt
```

This matches lines that **start with** `ERROR`.

Example:

```text
ERROR Database connection failed
```

But not:

```text
2026-08-16 ERROR Database connection failed
```

---

## Case 13: Match Lines Ending with a Keyword

Use the **`$`** anchor.

```bash
grep "failed$" logfile.txt
```

This matches lines that **end with** `failed`.

Example:

```text
Database connection failed
Authentication failed
```

---

## Case 14: Search All Files in a Directory

Use **`-r`** for recursive searching.

```bash
grep -r "database" dirA/
```

This searches files inside `dirA` and its subdirectories.

Example:

```bash
grep -r "server_name" /etc/nginx/
```

This is useful when searching configuration files.

---

## Case 15: Search Using Extended Regular Expressions

Use **`grep -E`** to work with extended regular expressions.

```bash
grep -E "ERROR|WARNING|FAILED" logfile.txt
```

This matches:

```text
ERROR
WARNING
FAILED
```

Older systems may also provide `egrep`:

```bash
egrep "ERROR|WARNING|FAILED" logfile.txt
```

However, **`grep -E` is preferred** because `egrep` is considered obsolete on many modern systems.

---

## Case 16: Search Without Printing Output

Use **`-q`** for quiet mode.

```bash
grep -q "ERROR" logfile.txt
```

No matching lines are displayed. GREP instead returns an **exit status**.

This is particularly useful in shell scripts.

Example:

```bash
if grep -q "ERROR" logfile.txt; then
    echo "Error found"
else
    echo "No error found"
fi
```

---

## Case 17: Search Command Output

GREP can also filter the output of another Linux command using a pipe.

```bash
ps aux | grep nginx
```

This searches the output of `ps aux` for `nginx`.

Another example:

```bash
df -h | grep "/dev"
```

This displays filesystem entries containing `/dev`.

---

## Case 18: Search Logs for Errors

GREP is commonly used for troubleshooting application and server logs.

```bash
grep "ERROR" application.log
```

Case-insensitive search:

```bash
grep -i "error" application.log
```

Show line numbers:

```bash
grep -in "error" application.log
```

Search multiple log files:

```bash
grep -i "error" /var/log/*.log
```

---

## Case 19: Search Multiple Patterns with Regular Expressions

Instead of using multiple `-e` options:

```bash
grep -E "ERROR|WARNING|FAILED" application.log
```

This is convenient when searching for several related log messages.

---

## Case 20: Suppress Error Messages

Use shell redirection to suppress error messages:

```bash
grep "ERROR" *.log 2>/dev/null
```

Here:

```text
2>/dev/null
```

redirects standard error messages to `/dev/null`.

---

## Common GREP Options

| Option | Description                  |
| ------ | ---------------------------- |
| `-i`   | Ignore case                  |
| `-v`   | Invert match                 |
| `-c`   | Count matching lines         |
| `-w`   | Match whole words            |
| `-n`   | Show line numbers            |
| `-r`   | Search recursively           |
| `-h`   | Hide filenames               |
| `-l`   | Show matching filenames only |
| `-e`   | Specify multiple patterns    |
| `-f`   | Read patterns from a file    |
| `-E`   | Extended regular expressions |
| `-q`   | Quiet mode                   |

---

## GREP with Common Linux Commands

GREP becomes especially powerful when combined with other commands.

### Find a Running Process

```bash
ps aux | grep nginx
```

### Find a Specific User

```bash
ps aux | grep rajesh
```

### Filter Disk Usage

```bash
df -h | grep "/dev"
```

### Filter Network Connections

```bash
ss -tulnp | grep 80
```

### Search Running Services

```bash
systemctl list-units | grep nginx
```

---

## GREP in Shell Scripts

GREP is frequently used in shell scripts to check whether a particular value or pattern exists.

Example:

```bash
if grep -q "ERROR" application.log; then
    echo "Error detected"
fi
```

This is useful for:

- Monitoring scripts
- Health checks
- Log monitoring
- Automated troubleshooting
- Alerting scripts

---

## Common Use Cases

- Search application logs
- Find errors and warnings
- Search configuration files
- Analyze server logs
- Search source code
- Filter command output
- Find specific processes
- Validate script output
- Troubleshoot production systems
- Build shell scripts and monitoring scripts

---

## Why GREP is Important

The **`grep`** command is one of the most important Linux text-processing utilities.

It allows you to quickly search large amounts of text and combine that search with other Linux commands using pipes.

A DevOps engineer commonly uses commands such as:

```bash
ps aux | grep nginx
df -h | grep "/dev"
cat application.log | grep ERROR
```

Understanding **`grep`**, regular expressions, pipes, and command combinations is essential for **Linux administration, shell scripting, DevOps, SRE, cloud operations, and production troubleshooting**.
