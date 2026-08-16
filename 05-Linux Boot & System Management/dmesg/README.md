# Linux `dmesg` Command

## What is `dmesg`?

`dmesg` is used to **display kernel-related messages retrieved from the kernel ring buffer**.

It is mainly useful for troubleshooting:

- Kernel issues
- Hardware detection
- Device drivers
- Disk and storage problems
- USB devices
- Network interfaces
- Boot-related issues
- Kernel errors and warnings

---

## Basic `dmesg` Command

Display all available kernel messages:

```bash
dmesg
```

---

## View Messages Page by Page

```bash
dmesg | more
```

Useful when the output is too long to fit on the terminal.

You can also use:

```bash
dmesg | less
```

`less` allows you to scroll both forward and backward through the output.

---

## Human-Readable Output

```bash
dmesg -HTx
```

Common options:

- `-H` → Human-readable output
- `-T` → Show human-readable timestamps
- `-x` → Show facility and log-level information

This makes kernel messages easier to understand.

---

## Filter Kernel Messages

Use `grep` to search for specific messages:

```bash
dmesg -HTx | grep "error"
```

For USB-related messages:

```bash
dmesg -HTx | grep "usb"
```

For disk-related messages:

```bash
dmesg -HTx | grep "disk"
```

For network-related messages:

```bash
dmesg -HTx | grep "network"
```

> The syntax `dmesg **-HTx | grep ——**` is not a valid command by itself. Replace the placeholder with a search pattern, such as `"error"`, `"usb"`, or `"disk"`.

---

## Monitor New Kernel Messages

```bash
dmesg -w
```

Continuously waits for and displays **new kernel messages as they are generated**.

This is useful for troubleshooting hardware.

For example:

```bash
dmesg -w
```

Then plug in a USB device and observe the new kernel messages.

---

## Clear the Kernel Ring Buffer

```bash
dmesg -c
```

Reads and clears the kernel ring buffer.

After running this command, previously stored messages are removed from the ring buffer.

> Use this carefully because clearing the buffer can remove useful troubleshooting information.

---

## Filter Messages by Log Level

You can filter kernel messages based on their log level.

### Alert Messages

```bash
dmesg -l alert
```

### Critical Messages

```bash
dmesg -l crit
```

### Error Messages

```bash
dmesg -l err
```

### Warning Messages

```bash
dmesg -l warning
```

### Informational Messages

```bash
dmesg -l info
```

### Multiple Log Levels

```bash
dmesg -l err,crit,alert
```

This displays messages with `error`, `critical`, or `alert` severity.

---

## Common Kernel Log Levels

| Level     | Meaning                          |
| --------- | -------------------------------- |
| `emerg`   | Emergency — system is unusable   |
| `alert`   | Immediate action required        |
| `crit`    | Critical condition               |
| `err`     | Error condition                  |
| `warning` | Warning condition                |
| `notice`  | Normal but significant condition |
| `info`    | Informational message            |
| `debug`   | Debugging information            |

---

## Common `dmesg` Commands

| Command                      | Purpose                                |
| ---------------------------- | -------------------------------------- |
| `dmesg`                      | Display kernel messages                |
| `dmesg \| more`              | View messages page by page             |
| `dmesg -HTx`                 | Display human-readable kernel messages |
| `dmesg -HTx \| grep "error"` | Filter messages containing `error`     |
| `dmesg -w`                   | Monitor new kernel messages            |
| `dmesg -c`                   | Read and clear the kernel ring buffer  |
| `dmesg -l err`               | Display error messages                 |
| `dmesg -l warning`           | Display warning messages               |
| `dmesg -l err,crit,alert`    | Display serious error messages         |

---

## Practical Troubleshooting Examples

### Check for Kernel Errors

```bash
dmesg -HTx | grep -i "error"
```

### Check USB Devices

```bash
dmesg -HTx | grep -i "usb"
```

### Check Disk Messages

```bash
dmesg -HTx | grep -Ei "disk|sda|nvme"
```

### Check Network-Related Messages

```bash
dmesg -HTx | grep -Ei "network|eth|ens|enp"
```

### Watch Hardware Events in Real Time

```bash
dmesg -w
```

---

## Quick Reference

```bash
# Display kernel messages
dmesg

# View page by page
dmesg | more

# Human-readable output
dmesg -HTx

# Filter messages
dmesg -HTx | grep "error"

# Monitor new messages
dmesg -w

# Clear kernel ring buffer
dmesg -c

# Filter by log level
dmesg -l alert
dmesg -l crit
dmesg -l err
dmesg -l warning
dmesg -l info

# Filter multiple levels
dmesg -l err,crit,alert
```

---

## Summary

`dmesg` is an important Linux troubleshooting command for viewing **kernel messages and hardware-related events**.

It is especially useful when diagnosing:

- **Boot problems**
- **Hardware issues**
- **Driver problems**
- **USB devices**
- **Disk/storage errors**
- **Network interfaces**
- **Kernel warnings and errors**
