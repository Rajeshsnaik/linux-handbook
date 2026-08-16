# SELinux

## What is SELinux?

**SELinux = Security-Enhanced Linux**

SELinux provides **Mandatory Access Control (MAC)** to add an additional security layer beyond normal Linux file and user permissions.

Even if normal Linux permissions allow access, **SELinux can still deny the operation** based on its security policy.

---

## SELinux Modes

Check the current SELinux mode:

```bash
getenforce
```

SELinux has three modes:

### Enforcing

```text
Enforcing
```

- SELinux is enabled.
- Unauthorized access is **blocked**.
- Violations are logged.

### Permissive

```text
Permissive
```

- SELinux is enabled.
- Unauthorized actions are **allowed**.
- Violations are logged.
- Useful for troubleshooting.

### Disabled

```text
Disabled
```

- SELinux is completely disabled.
- No SELinux policy enforcement occurs.

---

## Change SELinux Mode Temporarily

### Set Permissive Mode

```bash
setenforce 0
```

Changes SELinux from **Enforcing → Permissive**.

### Set Enforcing Mode

```bash
setenforce 1
```

Changes SELinux from **Permissive → Enforcing**.

> These changes are temporary and normally do not survive a reboot.

---

## Check SELinux Context

SELinux assigns security contexts to files, processes, and other resources.

Check file contexts:

```bash
ls -Z
```

Example:

```text
-rw-r--r--. root root system_u:object_r:httpd_sys_content_t:s0 index.html
```

---

## SELinux Context Structure

A typical SELinux context contains:

```text
user:role:type:level
```

Example:

```text
system_u:object_r:httpd_sys_content_t:s0
```

The four components are:

| Component | Example               | Purpose                   |
| --------- | --------------------- | ------------------------- |
| User      | `system_u`            | SELinux user              |
| Role      | `object_r`            | SELinux role              |
| Type      | `httpd_sys_content_t` | Defines the security type |
| Level     | `s0`                  | Security level            |

The **type** is particularly important because SELinux policies commonly use type-based access control to determine what a process can access.

---

## Restore Correct SELinux Context

If a file has an incorrect SELinux context, use:

```bash
restorecon filename
```

For example:

```bash
restorecon index.html
```

Restore contexts recursively:

```bash
restorecon -R /var/www/html
```

This restores the default SELinux contexts according to the system's policy.

---

## Permanent SELinux Configuration

The SELinux configuration file is:

```bash
/etc/selinux/config
```

Check the configuration:

```bash
cat /etc/selinux/config
```

The main setting is:

```bash
SELINUX=enforcing
```

Other possible values are:

```bash
SELINUX=permissive
```

or:

```bash
SELINUX=disabled
```

### Example

```text
SELINUX=enforcing
SELINUXTYPE=targeted
```

The configuration in `/etc/selinux/config` is applied across reboots.

---

## Temporary vs Permanent Configuration

| Command / Configuration | Effect                          |
| ----------------------- | ------------------------------- |
| `setenforce 0`          | Temporarily set Permissive      |
| `setenforce 1`          | Temporarily set Enforcing       |
| `/etc/selinux/config`   | Configure SELinux mode for boot |
| `getenforce`            | Check current mode              |

---

## Common SELinux Commands

```bash
# Check current mode
getenforce

# Set Permissive temporarily
setenforce 0

# Set Enforcing temporarily
setenforce 1

# View SELinux contexts
ls -Z

# Restore default context
restorecon filename

# Restore contexts recursively
restorecon -R /var/www/html

# Check permanent configuration
cat /etc/selinux/config
```

---

## SELinux Example

Suppose Nginx is serving files from:

```text
/var/www/html
```

Normal Linux permissions may allow Nginx to read a file.

However, if the file has an incorrect SELinux context, SELinux may still deny Nginx access.

Check the context:

```bash
ls -Z /var/www/html
```

Restore the expected context:

```bash
restorecon -R /var/www/html
```

This is a common troubleshooting step when a web server cannot access files even though normal Linux permissions appear correct.

---

## Interview Point

> **Even if normal Linux permissions allow access, SELinux can still deny it based on its security policy.**

Remember:

```text
Linux Permissions
       +
   SELinux Policy
       ↓
   Final Access
```

SELinux provides an additional security layer using **Mandatory Access Control (MAC)**.

---

## Quick Reference

```bash
# Check SELinux mode
getenforce

# Temporarily switch to Permissive
setenforce 0

# Temporarily switch to Enforcing
setenforce 1

# View SELinux file context
ls -Z

# Restore correct/default context
restorecon filename

# Restore recursively
restorecon -R /var/www/html

# Permanent configuration
/etc/selinux/config
```
