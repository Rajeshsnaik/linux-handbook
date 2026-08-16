# Linux Wildcards & Regular Expressions (Regex)

## What are Wildcards?

**Wildcards** are special characters used to match file and directory names in commands such as `ls`, `cp`, `mv`, and `rm`.

---

## Common Wildcards

### `*` — Zero or More Characters

```bash id="e1f5p7"
ls *.txt
cp *.log /backup/
rm *.tmp
```

---

### `?` — Exactly One Character

```bash id="pt2d4v"
ls file?.txt
```

Matches:

```text id="z4vm3h"
file1.txt
fileA.txt
```

Does not match:

```text id="1xczgw"
file10.txt
```

---

### `[]` — Match Characters or Range

```bash id="as8x3p"
ls [abc]*
ls file[1-5].txt
```

---

### `[!]` — Negation

Match files that do not start with `a`:

```bash id="x5pkpj"
ls [!a]*
```

---

### `{}` — Generate Multiple Names

```bash id="c3u2xr"
touch file{1..5}.txt
```

Creates:

```text id="7ll8zp"
file1.txt
file2.txt
file3.txt
file4.txt
file5.txt
```

Create multiple directories:

```bash id="59m0km"
mkdir -p project/{src,docs,images}
```

---

# What is Regex?

A **Regular Expression (Regex)** is a pattern used to search and match text. It is commonly used with:

```text id="p3fcpd"
grep
sed
awk
```

---

## Common Regex Patterns

| Pattern | Meaning              | Example                            |
| ------- | -------------------- | ---------------------------------- |
| `^`     | Start of line        | `grep "^ERROR" file.txt`           |
| `$`     | End of line          | `grep "failed$" file.txt`          |
| `.`     | Any single character | `grep "c.t" file.txt`              |
| `*`     | Zero or more         | `grep "ab*c" file.txt`             |
| `+`     | One or more          | `grep -E "ab+c" file.txt`          |
| `?`     | Optional character   | `grep -E "colou?r" file.txt`       |
| `[a-z]` | Lowercase letters    | `grep "[a-z]" file.txt`            |
| `[0-9]` | Digits               | `grep "[0-9]" file.txt`            |
| `\|`    | OR condition         | `grep -E "ERROR\|FAILED" file.txt` |

---

## Useful Regex Examples

### Start of Line

```bash id="7y5nkj"
grep "^ERROR" logfile.txt
```

### End of Line

```bash id="qplx6h"
grep "failed$" logfile.txt
```

### Case-Insensitive Search

```bash id="qbr5o6"
grep -i "linux" file.txt
```

### Match Exact Word

```bash id="7s9j3s"
grep -w "Linux" file.txt
```

### Match Multiple Patterns

```bash id="e4n2mj"
grep -E "ERROR|WARNING|FAILED" logfile.txt
```

---

# Wildcards vs Regex

| Wildcards                 | Regular Expressions                |
| ------------------------- | ---------------------------------- |
| Used mainly for filenames | Used for text patterns             |
| Handled by the shell      | Used by `grep`, `sed`, `awk`       |
| Simpler                   | More powerful                      |
| `*`, `?`, `[]`            | `^`, `$`, `.`, `*`, `+`, `?`, `[]` |

---

## Common Use Cases

### Wildcards

- List multiple files
- Copy or move files
- Delete matching files
- Create multiple files/directories

### Regex

- Search logs
- Filter command output
- Find errors
- Process text
- Automate scripts

---

## Why Learn Wildcards & Regex?

**Wildcards** make file operations faster, while **Regex** provides powerful text searching and pattern matching.

Both are essential for **Linux administration, log analysis, shell scripting, automation, and DevOps**.
