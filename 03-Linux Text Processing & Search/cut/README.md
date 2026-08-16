# `cut` Command

The **`cut`** command is used to **extract specific fields, columns, or characters from text**.

It is commonly used with structured data such as `/etc/passwd`, CSV files, logs, and command output.

---

## Syntax

```bash
cut [options] file
```

---

## Extract Fields

Use `-d` to specify the delimiter and `-f` to select the field.

```bash
cut -d: -f1 /etc/passwd
```

- `-d:` → `:` is the delimiter
- `-f1` → extract field 1

Example:

```bash
echo "Rajesh:DevOps:3" | cut -d: -f2
```

Output:

```text
DevOps
```

### Multiple Fields

```bash
echo "Rajesh:DevOps:3" | cut -d: -f1,3
```

Output:

```text
Rajesh:3
```

### Field Range

```bash
echo "Rajesh:DevOps:3:AWS" | cut -d: -f1-3
```

Output:

```text
Rajesh:DevOps:3
```

---

## Extract Characters

Use `-c` to extract specific characters.

```bash
echo "Rajesh" | cut -c1-3
```

Output:

```text
Raj
```

Extract from character 3 to the end:

```bash
echo "Rajesh" | cut -c3-
```

Output:

```text
jesh
```

---

## Important Options

| Option         | Meaning                                   |
| -------------- | ----------------------------------------- |
| `-d`           | Specify delimiter                         |
| `-f`           | Select fields/columns                     |
| `-c`           | Select characters                         |
| `-s`           | Suppress lines without delimiter          |
| `--complement` | Select everything except specified fields |

---

## Real-World Examples

### Get Linux Usernames

```bash
cut -d: -f1 /etc/passwd
```

### Get User Home Directories

```bash
cut -d: -f6 /etc/passwd
```

### Extract CSV Column

```bash
cut -d',' -f2 users.csv
```

### Extract IP Address

```bash
hostname -I | cut -d' ' -f1
```

### Combine with `grep`

```bash
grep "DevOps" users.txt | cut -d: -f3
```

---

## `cut` vs `awk`

`cut` is best for **simple column or character extraction**.

```bash
cut -d: -f1 /etc/passwd
```

`awk` is better when you need **conditions, calculations, or more complex processing**.

```bash
awk -F: '{print $1}' /etc/passwd
```

---

## Interview Point

> **`cut` is a Linux command used to extract specific fields, columns, or characters from text. The `-d` option specifies the delimiter, `-f` selects fields, and `-c` selects characters.**

### Easy Way to Remember

```text
cut
 │
 ├── -d → Delimiter
 ├── -f → Fields
 └── -c → Characters
```

**Example:**

```bash
echo "Rajesh:DevOps:3" | cut -d: -f2
```

Output:

```text
DevOps
```
