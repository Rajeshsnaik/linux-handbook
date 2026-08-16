# Linux Pipe, `tee`, and `xargs`

## What is Pipe in Linux?

A **pipe (`|`)** connects the output of one command to the input of another command.

```bash
command1 | command2
```

The output (**stdout**) of `command1` becomes the input (**stdin**) of `command2`.

You can chain multiple commands:

```bash
command1 | command2 | command3
```

Pipes are commonly used for **filtering, searching, sorting, and processing data**.

---

## Common Pipe Examples

### Count Files

```bash
ls | wc -l
```

Count regular files recursively:

```bash
find . -type f | wc -l
```

### Sort Combined Files

```bash
cat file1.txt file2.txt | sort
```

Reverse order:

```bash
cat file1.txt file2.txt | sort -r
```

### Remove Duplicate Lines

```bash
sort data.txt | uniq
```

Only duplicate lines:

```bash
sort data.txt | uniq -d
```

Only lines that appear once:

```bash
sort data.txt | uniq -u
```

### View Specific Lines

```bash
head -20 file.txt | tail -11
```

Or:

```bash
sed -n '10,20p' file.txt
```

### View Large Files

```bash
cat largefile.txt | less
```

Usually, the simpler form is:

```bash
less largefile.txt
```

---

# What is `tee` Command?

The **`tee`** command reads input from `stdin` and writes it to both:

1. The terminal
2. A file

### Syntax

```bash
command | tee filename
```

### Save Output to a File

```bash
ls -l | tee files.txt
```

The output is displayed on the terminal and saved in `files.txt`.

### Append to a File

Use `-a`:

```bash
date | tee -a logfile.txt
```

This appends instead of overwriting the file.

### Save to Multiple Files

```bash
echo "Linux" | tee file1.txt file2.txt
```

### Common Uses

- Save command output while viewing it
- Capture logs
- Debug shell scripts
- Save output to multiple files

---

# What is `xargs` Command?

The **`xargs`** command takes input from `stdin` and converts it into **arguments for another command**.

### Syntax

```bash
command | xargs another_command
```

For example:

```bash
echo "file1 file2 file3" | xargs rm
```

This effectively runs:

```bash
rm file1 file2 file3
```

---

## Common `xargs` Examples

### Process Files Found by `find`

```bash
find . -name "*.txt" | xargs ls -l
```

### Search Multiple Files

```bash
find . -name "*.log" | xargs grep "ERROR"
```

### Count Lines in Multiple Files

```bash
find . -name "*.txt" | xargs wc -l
```

> For filenames containing spaces or special characters, prefer null-delimited input:

```bash
find . -name "*.log" -print0 | xargs -0 grep "ERROR"
```

---

# Pipe vs `tee` vs `xargs`

| Command | Purpose                              |
| ------- | ------------------------------------ |
| `\|`    | Pass output to another command       |
| `tee`   | Display output and save it to a file |
| `xargs` | Convert input into command arguments |

---

## How They Work

```text
Command 1
   │
   │ Output
   ▼
  Pipe (|)
   │
   ▼
Command 2
   │
   ├──► tee ──► File
   │
   └──► xargs ──► Command Arguments
```

---

## Interview Point

**Pipe (`|`)**:

> Passes the output of one command as input to another command.

**`tee`**:

> Displays command output while simultaneously writing it to a file.

**`xargs`**:

> Converts input from standard input into arguments for another command.

### Easy Way to Remember

```text
|     → Connect commands
tee   → View + Save
xargs → Input → Arguments
```

These are fundamental Linux tools used extensively in **shell scripting, system administration, DevOps, automation, and troubleshooting**.
