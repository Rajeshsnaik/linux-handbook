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
