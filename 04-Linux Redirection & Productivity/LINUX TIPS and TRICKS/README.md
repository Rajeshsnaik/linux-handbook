# Linux Tips and Tricks to Improve Productivity

## Tab for Autocompletion

Press the **Tab** key to automatically complete commands, file names, and directory names.

If multiple matches exist, press **Tab** twice to display all possible options.

```bash id="3d9kq8"
cd /var/lo<Tab>
```

Tab completion reduces typing and helps avoid spelling mistakes.

---

## Switch to Last Working Directory

Use **`cd -`** to quickly switch back to the previous directory.

```bash id="1qv4yo"
cd -
```

This is useful when frequently moving between two directories.

---

## Running Multiple Commands in a Single Line

Linux allows you to execute multiple commands using command separators.

### Run commands regardless of previous result

Use `;`:

```bash id="b8g5nu"
pwd ; date ; whoami
```

Each command runs sequentially, regardless of whether the previous command succeeds or fails.

### Run the next command only if the previous succeeds

Use `&&`:

```bash id="1l5r8w"
mkdir demo && cd demo
```

The second command runs only if `mkdir demo` succeeds.

### Run the next command only if the previous fails

Use `||`:

```bash id="w7a3mc"
mkdir demo || echo "Directory already exists"
```

The second command runs only if `mkdir demo` fails.

---

## Read Large Files

Use **`less`** to view large files efficiently.

```bash id="8zq4qv"
less largefile.log
```

Useful shortcuts inside `less`:

- `Space` → Next page
- `b` → Previous page
- `/text` → Search
- `n` → Next search result
- `q` → Quit

---

## Empty a File Without Deleting It

Clear the contents of a file while keeping the file itself.

```bash id="x7k1s4"
> logfile.log
```

Or:

```bash id="2v6m8a"
truncate -s 0 logfile.log
```

This is useful for clearing log files without deleting the file.

---

## Live Monitoring Using `tail -f`

Monitor new content added to a file in real time.

```bash id="m4q8tz"
tail -f logfile.log
```

Useful for monitoring:

- Application logs
- Nginx logs
- Apache logs
- System logs
- Service logs

Press **Ctrl + C** to stop monitoring.

---

## Record All Terminal Commands

Use the **`script`** command to record a terminal session.

Start recording:

```bash id="5n2x8j"
script terminal.log
```

Perform your commands normally.

Stop recording:

```bash id="7c3m1p"
exit
```

The terminal session and its output are saved in `terminal.log`.

---

## Use Calculator in Linux

Use the **`bc`** command for calculations.

### Addition

```bash id="4j9z2k"
echo "25+15" | bc
```

### Division

```bash id="9v6x1c"
echo "100/5" | bc
```

### Floating-Point Calculation

```bash id="3y7p5m"
echo "scale=2;10/3" | bc
```

---

## Move Cursor to Start or End of Command

Useful Bash keyboard shortcuts:

- **Ctrl + A** → Move to beginning of line
- **Ctrl + E** → Move to end of line

These are especially useful when editing long commands.

---

## Clear Current Command and Redo

Use these shortcuts to quickly edit the current command:

- **Ctrl + U** → Delete from cursor to beginning
- **Ctrl + K** → Delete from cursor to end
- **Ctrl + Y** → Paste deleted text back

These shortcuts make command-line editing much faster.

---

## Reverse Search Previous Commands

Press:

```text
Ctrl + R
```

Then type part of a previous command.

For example, search for a previous SSH command:

```text
(reverse-i-search)`ssh':
```

Press **Ctrl + R** repeatedly to cycle through matching commands.

Press **Enter** to execute the selected command.

---

## Clear the Terminal Screen

Use the keyboard shortcut:

```text
Ctrl + L
```

Or use:

```bash id="z9q3pk"
clear
```

Both clear the visible terminal screen.

> **Note:** Clearing the screen does not delete your command history.

---

## Delete One Character from the Left

Use:

```text
Backspace
```

Or:

```text
Ctrl + H
```

Both delete one character before the cursor.

---

## Switch to Home Directory

Quickly return to your home directory:

```bash id="j5x8pq"
cd
```

or:

```bash id="r4k6nv"
cd ~
```

This works from any location.

---

## History Command

Display previously executed commands:

```bash id="7x2n9m"
history
```

### Run a Command Using Its History Number

```bash id="k3v7qa"
!100
```

This executes command number `100` from the history.

### Repeat the Last Command

```bash id="d8w2hm"
!!
```

### Search Command History

```bash id="p5n1yr"
history | grep ssh
```

This displays previous commands containing `ssh`.

---

## Most Useful Keyboard Shortcuts

| Shortcut   | Description                      |
| ---------- | -------------------------------- |
| `Tab`      | Auto-complete commands and files |
| `Ctrl + A` | Move to beginning of line        |
| `Ctrl + E` | Move to end of line              |
| `Ctrl + U` | Delete to beginning              |
| `Ctrl + K` | Delete to end                    |
| `Ctrl + Y` | Paste deleted text               |
| `Ctrl + R` | Reverse command search           |
| `Ctrl + L` | Clear terminal screen            |
| `Ctrl + C` | Stop a running command           |
| `Ctrl + D` | Exit shell / logout              |
| `Ctrl + Z` | Suspend current process          |
| `Ctrl + H` | Delete character before cursor   |

---

## Why These Tips Matter

These Linux productivity tips help you work faster by:

- Reducing repetitive typing
- Simplifying directory navigation
- Improving command history usage
- Making command editing faster
- Monitoring logs efficiently
- Managing files more effectively
- Improving troubleshooting workflows
- Reducing command-line errors

Mastering these shortcuts and techniques can significantly improve your daily workflow as a **Linux administrator, DevOps engineer, cloud engineer, or developer**.

---

## Quick Productivity Reference

```bash id="r2w6kt"
# Go to previous directory
cd -

# Go to home directory
cd ~

# View large file
less logfile.log

# Follow log file
tail -f logfile.log

# Clear a file
> logfile.log

# Calculator
echo "25+15" | bc

# Show command history
history

# Search history
history | grep ssh

# Repeat last command
!!

# Run command by history number
!100

# Clear terminal
clear
```
