# Linux `systemctl` Commands

## What is `systemctl`?

`systemctl` is the command-line utility used to **manage and control systemd services** on Linux.

It can be used to:

- Start and stop services
- Restart and reload services
- Check service status
- Enable or disable services at boot
- Mask or unmask services
- Check whether a service is enabled
- Manage systemd units

---

## Check Service Status

Check the current status of a service:

```bash
systemctl status nginx
```

---

## Start a Service

Start a stopped service:

```bash
systemctl start nginx
```

---

## Stop a Service

Stop a running service:

```bash
systemctl stop nginx
```

---

## Restart a Service

Restart a service completely:

```bash
systemctl restart nginx
```

Useful when configuration or application changes require a full restart.

---

## Reload a Service

Reload the service configuration without completely stopping the service:

```bash
systemctl reload nginx
```

Useful for services such as Nginx where you want to apply configuration changes without interrupting existing connections.

---

## Enable a Service

Configure a service to start automatically when the system boots:

```bash
systemctl enable nginx
```

---

## Enable and Start a Service

Enable the service at boot **and start it immediately**:

```bash
systemctl enable --now nginx
```

This is commonly used when installing and configuring a new service.

---

## Disable a Service

Prevent a service from starting automatically during boot:

```bash
systemctl disable nginx
```

This does **not** stop the service if it is currently running.

To stop it as well:

```bash
systemctl disable --now nginx
```

---

## Mask a Service

Prevent a service from being started manually or automatically:

```bash
systemctl mask nginx
```

A masked service cannot be started until it is unmasked.

---

## Unmask a Service

Allow a previously masked service to be started again:

```bash
systemctl unmask nginx
```

---

## Check if a Service is Enabled

Check whether a service is configured to start automatically at boot:

```bash
systemctl is-enabled nginx
```

Possible results include:

```text
enabled
disabled
masked
static
```

---

## Check if a Service is Active

Check whether a service is currently running:

```bash
systemctl is-active nginx
```

Possible results:

```text
active
inactive
failed
```

---

## List Running Services

Display currently running services:

```bash
systemctl list-units --type=service --state=running
```

---

## List All Services

Display loaded service units:

```bash
systemctl list-units --type=service
```

---

## List Failed Services

Find services that have failed:

```bash
systemctl --failed
```

---

## View Service Logs

`systemctl` can be used together with `journalctl` to investigate service logs:

```bash
journalctl -u nginx
```

View recent logs:

```bash
journalctl -u nginx -n 50
```

Follow logs in real time:

```bash
journalctl -u nginx -f
```

---

## Common `systemctl` Commands

| Command                         | Purpose                       |
| ------------------------------- | ----------------------------- |
| `systemctl status nginx`        | Check service status          |
| `systemctl start nginx`         | Start service                 |
| `systemctl stop nginx`          | Stop service                  |
| `systemctl restart nginx`       | Restart service               |
| `systemctl reload nginx`        | Reload configuration          |
| `systemctl enable nginx`        | Enable at boot                |
| `systemctl disable nginx`       | Disable at boot               |
| `systemctl enable --now nginx`  | Enable and start              |
| `systemctl disable --now nginx` | Disable and stop              |
| `systemctl mask nginx`          | Prevent service from starting |
| `systemctl unmask nginx`        | Allow service to start        |
| `systemctl is-enabled nginx`    | Check boot status             |
| `systemctl is-active nginx`     | Check running status          |
| `systemctl --failed`            | List failed units             |

---

## Typical Service Management Workflow

For a newly installed service:

```bash
systemctl status nginx
systemctl start nginx
systemctl enable nginx
```

Or use a single command:

```bash
systemctl enable --now nginx
```

After changing configuration:

```bash
systemctl reload nginx
```

If the service is not working correctly:

```bash
systemctl status nginx
journalctl -u nginx -n 50
```

---

## Quick Reference

```bash
# Status
systemctl status nginx

# Start
systemctl start nginx

# Stop
systemctl stop nginx

# Restart
systemctl restart nginx

# Reload configuration
systemctl reload nginx

# Enable at boot
systemctl enable nginx

# Disable at boot
systemctl disable nginx

# Enable + start
systemctl enable --now nginx

# Disable + stop
systemctl disable --now nginx

# Mask
systemctl mask nginx

# Unmask
systemctl unmask nginx

# Check enabled
systemctl is-enabled nginx

# Check running
systemctl is-active nginx

# Failed services
systemctl --failed

# Service logs
journalctl -u nginx
```
