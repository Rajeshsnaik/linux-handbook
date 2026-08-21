# Linux `top` Command

## What is `top`?

`top` is a command-line utility used to display a **real-time view of running processes** in Linux.

It continuously updates the process list and shows important system information such as:

- CPU usage
- Memory usage
- Process ID (PID)
- Process owner
- Process priority
- Process state
- Running processes

---

## Start `top`

```bash
top
```

The `top` interface continuously refreshes and displays currently running processes.

Press:

```text
q
```

to exit `top`.

---

## Useful `top` Interactive Commands

The following commands are entered **while `top` is running**.

### `c` — Show Full Command Path

Press:

```text
c
```

Toggles the command column between the process name and the **full command/command-line path**.

---

### `k` — Kill a Process

Press:

```text
k
```

`top` will ask for the **PID** of the process you want to terminate.

Example:

```text
PID to kill: 1234
```

You may then be prompted for a signal. The default is commonly `15` (`SIGTERM`), which requests a graceful termination.

---

### `n` — Change Number of Tasks

Press:

```text
n
```

Allows you to specify how many processes/tasks should be displayed.

Example:

```text
Maximum tasks = 10
```

---

### `d` / `s` — Change Refresh Interval

Press:

```text
d
```

or:

```text
s
```

to change the **delay/refresh interval**.

For example:

```text
Change delay from 3.0 to: 1
```

This makes `top` refresh every 1 second.

> On many versions of `top`, `d` is the standard key for changing the delay. `s` can also have a different meaning depending on the `top` version/configuration.

---

### `M` — Sort by Memory Usage

Press:

```text
M
```

Sorts processes based on **memory usage**.

This is useful when you want to find processes consuming the most RAM.

---

### `r` — Change Process Priority

Press:

```text
r
```

Allows you to change the **nice value** of a process.

You first provide the PID and then the new nice value.

Example:

```text
PID to renice: 1234
Renice PID 1234 to value: 10
```

### Nice Value

The nice value normally ranges from:

```text
-20 → 19
```

- **-20** → Highest priority
- **0** → Default priority
- **19** → Lowest priority

In general:

> **Lower nice value = higher CPU scheduling priority**

Changing a process to a negative nice value usually requires appropriate privileges.

---

### `u` — Filter by User

Press:

```text
u
```

Allows you to enter a username and display processes belonging to that user.

Example:

```text
Which user (blank for all): rajesh
```

This is useful when you want to monitor processes belonging to a particular user.

---

### `h` — Help

Press:

```text
h
```

Displays the **help screen** with available `top` commands and interactive options.

---

## Common `top` Interactive Commands

| Key | Purpose                                  |
| --- | ---------------------------------------- |
| `c` | Toggle full command/command-line display |
| `k` | Kill a process by PID                    |
| `n` | Change number of tasks displayed         |
| `d` | Change refresh/delay interval            |
| `M` | Sort by memory usage                     |
| `r` | Change process nice value                |
| `u` | Filter processes by user                 |
| `h` | Display help                             |
| `q` | Exit `top`                               |

---

## Process Priority

Linux uses the **nice value** to influence CPU scheduling priority.

```text
Nice Value

-20  ← Highest priority
  0  ← Default
 19  ← Lowest priority
```

Example:

```text
nice -20 → Higher priority
nice  10 → Lower priority
```

A process with a lower nice value generally receives more favorable CPU scheduling compared with a process with a higher nice value.

---

## Useful `top` Workflow

Start `top`:

```bash
top
```

Then use interactive commands:

```text
c  → Show full command
M  → Sort by memory
u  → Filter by user
k  → Kill process
r  → Change priority
d  → Change refresh interval
n  → Change number of tasks
h  → Show help
q  → Exit
```

---

## `top` vs `ps`

| Command | Description                                     |
| ------- | ----------------------------------------------- |
| `ps`    | Provides a snapshot of processes                |
| `top`   | Provides a continuously updating real-time view |

For example:

```bash
ps aux
```

shows the processes at that moment, while:

```bash
top
```

continually refreshes the process information.

---

## Quick Reference

```bash
# Start real-time process monitor
top

# While inside top:

c   # Show full command
k   # Kill process by PID
n   # Change number of tasks
d   # Change refresh interval
M   # Sort by memory usage
r   # Change nice value
u   # Filter by user
h   # Show help
q   # Exit
```

## Interview Point

> **`top` is a real-time Linux process monitoring tool used to view running processes and their CPU, memory, PID, user, priority, and process-state information.**
