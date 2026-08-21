# Linux Process Management

## What is Process Management?

**Process management** is the process of controlling and monitoring programs running on a Linux system.

Linux provides commands to:

- View background and foreground jobs
- Move processes between foreground and background
- Keep processes running after logout
- Control process priority
- Monitor process IDs (PIDs)

Common process management commands include:

```text
jobs
bg
fg
nohup
nice
```

---

# `jobs`

The `jobs` command displays jobs started from the **current shell**.

```bash
jobs
```

Display jobs with their process IDs:

```bash
jobs -l
```

Example:

```text
[1]+  1234 Running    python3 app.py &
[2]-  1235 Stopped    vim file.txt
```

Here:

- `[1]` → Job ID
- `1234` → Process ID (PID)
- `Running` → Current job state

> `jobs` shows jobs associated with the current shell, not every process running on the system.

---

# Background and Foreground Jobs

Linux shell jobs can run in two main modes:

### Foreground

The terminal is occupied by the running process.

```bash
python3 app.py
```

You can usually press:

```text
Ctrl + C
```

to terminate the foreground process.

### Background

The process runs without blocking the terminal.

```bash
python3 app.py &
```

The `&` sends the command to the background.

---

# `bg`

The `bg` command resumes a **stopped job in the background**.

```bash
bg
```

Resume a specific job:

```bash
bg %<job-id>
```

Example:

```bash
bg %1
```

If a foreground process is stopped using:

```text
Ctrl + Z
```

you can continue it in the background with:

```bash
bg %1
```

---

# `fg`

The `fg` command brings a background or stopped job to the **foreground**.

```bash
fg
```

Bring a specific job to the foreground:

```bash
fg %<job-id>
```

Example:

```bash
fg %1
```

---

# `jobs`, `bg`, and `fg` Example

Start a process:

```bash
python3 app.py
```

Press:

```text
Ctrl + Z
```

The process becomes stopped.

Check the job:

```bash
jobs -l
```

Resume it in the background:

```bash
bg %1
```

Bring it back to the foreground:

```bash
fg %1
```

---

# `nohup`

`nohup` means **No Hang Up**.

It allows a command to continue running even after the terminal session is closed or the user logs out.

Basic syntax:

```bash
nohup process &
```

Example:

```bash
nohup python3 app.py &
```

This is useful for long-running commands or applications when you do not want them to terminate when the terminal disconnects.

> `nohup` protects the process from the terminal's hangup signal (`SIGHUP`), but it is not a complete process supervisor. For production services, tools such as `systemd`, Docker, or a dedicated process manager are generally more appropriate.

---

## `nohup.out`

By default, when output is not redirected elsewhere, `nohup` writes the command's output to:

```text
nohup.out
```

For example:

```bash
nohup python3 app.py &
```

Output can be written to:

```text
nohup.out
```

---

## Redirect `nohup` Output

You can specify your own log file:

```bash
nohup python3 app.py > app.log 2>&1 &
```

Here:

- `>` → Redirect standard output (`stdout`)
- `app.log` → Output file
- `2>` → Redirect standard error (`stderr`)
- `&1` → Send `stderr` to the same location as `stdout`
- `&` → Run the command in the background

Therefore, both standard output and errors are written to:

```text
app.log
```

---

# `nice`

`nice` is used to start a process with a specified **nice value**.

The nice value influences the process's CPU scheduling priority.

Basic syntax:

```bash
nice -n 5 process
```

Example:

```bash
nice -n 5 python3 app.py
```

---

## Nice Value Range

The normal nice value range is:

```text
-20  → Highest priority
  0  → Default priority
 19  → Lowest priority
```

### Important Rule

> **Lower nice value = higher CPU scheduling priority.**

For example:

```text
nice -10  → Higher priority
nice   0  → Normal priority
nice  10  → Lower priority
```

Starting a process with a negative nice value generally requires elevated privileges.

---

# Find a Process PID

You can use `ps` to find the PID of a process.

```bash
ps -ef | grep httpd
```

Example:

```text
root    1234    1  0 10:20 ?  00:00:01 /usr/sbin/httpd
```

Here:

```text
PID = 1234
```

For more reliable process lookup, you can also use:

```bash
pgrep httpd
```

---

# Common Process Management Commands

| Command             | Purpose                                |
| ------------------- | -------------------------------------- |
| `jobs`              | Show current shell jobs                |
| `jobs -l`           | Show jobs with PIDs                    |
| `bg`                | Resume a stopped job in the background |
| `bg %1`             | Resume job 1 in background             |
| `fg`                | Bring a job to the foreground          |
| `fg %1`             | Bring job 1 to foreground              |
| `nohup command &`   | Keep command running after logout      |
| `nice -n 5 command` | Start command with nice value 5        |
| `ps -ef`            | View processes and PIDs                |
| `pgrep httpd`       | Find PID of `httpd`                    |

---

# Practical Example

Start a Python application with `nohup` and save its logs:

```bash
nohup python3 app.py > app.log 2>&1 &
```

Check the process:

```bash
ps -ef | grep app.py
```

Or:

```bash
pgrep -af app.py
```

Check the log:

```bash
tail -f app.log
```

The application can continue running even after the terminal session is closed.

---

# Quick Reference

```bash
# View current shell jobs
jobs

# View jobs with PIDs
jobs -l

# Resume job in background
bg

# Resume specific job
bg %1

# Bring job to foreground
fg

# Bring specific job to foreground
fg %1

# Run command in background
command &

# Keep process running after logout
nohup command &

# Run application with custom log file
nohup python3 app.py > app.log 2>&1 &

# Start process with nice value
nice -n 5 python3 app.py

# Find process PID
ps -ef | grep httpd

# Find process PID more directly
pgrep httpd
```

---

## Interview Points

- **`jobs`** → Shows jobs belonging to the current shell.
- **`bg`** → Resumes a stopped job in the background.
- **`fg`** → Brings a background/stopped job to the foreground.
- **`nohup`** → Prevents a command from being terminated by a terminal hangup.
- **`nice`** → Starts a process with a specified scheduling niceness.
- **Nice range:** `-20` to `19`.
- **Lower nice value = higher CPU scheduling priority.**
- **`nohup.out`** → Default output file when `nohup` output is not redirected.
