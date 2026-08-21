# Linux Process Status — `ps`

## What is `ps`?

`ps` stands for **Process Status**.

It is used to **display information about processes running on a Linux system**.

It is useful for:

- Viewing running processes
- Finding a specific process
- Checking which user owns a process
- Checking CPU and memory usage
- Understanding parent-child process relationships
- Troubleshooting services and applications

---

## Display All Running Processes

### `ps -e`

```bash
ps -e
```

Displays **all processes** currently running on the system.

---

### `ps -A`

```bash
ps -A
```

Also displays **all processes**.

`-A` and `-e` are commonly used for the same purpose.

---

## Display Detailed Process Information

### `ps -ef`

```bash
ps -ef
```

Displays all processes in a **full-format listing**.

Example output:

```text
UID   PID   PPID  C  STIME  TTY      TIME     CMD
root  1234  1     0  10:20  ?        00:00:01 nginx
```

Important columns:

| Column  | Meaning                          |
| ------- | -------------------------------- |
| `UID`   | User who owns the process        |
| `PID`   | Process ID                       |
| `PPID`  | Parent Process ID                |
| `C`     | CPU utilization                  |
| `STIME` | Start time                       |
| `TTY`   | Terminal associated with process |
| `TIME`  | CPU time used                    |
| `CMD`   | Command that started the process |

---

## Display Processes with CPU and Memory Usage

### `ps aux`

```bash
ps aux
```

Displays detailed information about all processes, including:

- CPU usage
- Memory usage
- Process owner
- Process ID
- Start time
- Command

Important columns include:

| Column    | Meaning             |
| --------- | ------------------- |
| `USER`    | Process owner       |
| `PID`     | Process ID          |
| `%CPU`    | CPU usage           |
| `%MEM`    | Memory usage        |
| `VSZ`     | Virtual memory size |
| `RSS`     | Resident memory     |
| `STAT`    | Process state       |
| `START`   | Start time          |
| `COMMAND` | Command             |

---

## Find a Specific Process

```bash
ps -ef | grep httpd
```

Searches the process list for processes containing `httpd`.

For example, this can be used to check whether an Apache HTTP server process is running.

> `grep` itself may also appear in the output because the search command contains `httpd`.

---

## Display Processes of a Specific User

```bash
ps -u <user-name>
```

Example:

```bash
ps -u rajesh
```

Displays processes owned by the specified user.

---

## Display Processes Belonging to a Group

```bash
ps -G <grp-name>
```

Example:

```bash
ps -G developers
```

Displays processes associated with the specified group.

---

## Display Process Hierarchy

```bash
ps -ejH
```

Displays processes in a **hierarchical format**, showing parent-child relationships.

This is useful for understanding which process started another process.

Example:

```text
systemd
 ├── sshd
 │    └── bash
 │         └── vim
 └── nginx
      ├── nginx
      └── nginx
```

---

## Common `ps` Commands

| Command                | Purpose                                   |
| ---------------------- | ----------------------------------------- |
| `ps -e`                | Display all processes                     |
| `ps -A`                | Display all processes                     |
| `ps -ef`               | Display all processes in full format      |
| `ps aux`               | Display detailed process information      |
| `ps -ef \| grep httpd` | Find `httpd` processes                    |
| `ps -u <user-name>`    | Display user's processes                  |
| `ps -G <grp-name>`     | Display processes associated with a group |
| `ps -ejH`              | Display process hierarchy                 |

---

## `ps` vs `top`

`ps` provides a **snapshot** of the processes at the time the command is executed.

```bash
ps aux
```

`top` provides a **real-time, continuously updating** view of processes.

```bash
top
```

---

## Quick Reference

```bash
# All processes
ps -e

# All processes
ps -A

# Full process information
ps -ef

# Detailed process information
ps aux

# Find a specific process
ps -ef | grep httpd

# Processes of a user
ps -u <user-name>

# Processes associated with a group
ps -G <grp-name>

# Process hierarchy
ps -ejH
```

## Interview Point

> **`ps` is used to take a snapshot of currently running processes and inspect information such as PID, PPID, user, CPU usage, memory usage, and the command that started the process.**
