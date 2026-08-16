# Cockpit

## What is Cockpit?

**Cockpit** is a **web-based Linux server management and monitoring tool**.

It provides a graphical interface that allows administrators to manage and monitor Linux servers through a **web browser instead of using only the terminal**.

Cockpit is commonly used for server administration, monitoring, troubleshooting, and managing system resources.

---

## What Can You Do with Cockpit?

Cockpit provides a web interface for tasks such as:

- Monitor CPU usage
- Monitor memory usage
- Monitor disk usage
- Manage system services
- View system logs
- Manage users
- Manage storage
- Check network configuration
- Open a terminal
- Monitor system performance

---

## Cockpit Web Interface

Cockpit normally runs on port **9090**.

Access it using:

```text
https://<server-ip>:9090
```

Example:

```text
https://192.189.1.100:9090
```

You can then log in using a Linux user account with the required permissions.

---

## Enable Cockpit

Cockpit uses a systemd socket called `cockpit.socket`.

Enable and start it:

```bash
sudo systemctl enable --now cockpit.socket
```

This:

- Enables Cockpit to start automatically when required
- Starts the Cockpit socket immediately

---

## Check Cockpit Status

```bash
systemctl status cockpit.socket
```

This shows whether the Cockpit socket is active and running.

---

## Check Cockpit Socket

You can also check whether the socket is listening:

```bash
systemctl status cockpit.socket
```

Or check port `9090`:

```bash
ss -tulpn | grep 9090
```

---

## Common Cockpit Commands

```bash
# Enable and start Cockpit
sudo systemctl enable --now cockpit.socket

# Check Cockpit status
systemctl status cockpit.socket

# Stop Cockpit
sudo systemctl stop cockpit.socket

# Start Cockpit
sudo systemctl start cockpit.socket

# Restart Cockpit
sudo systemctl restart cockpit.socket
```

---

## Cockpit vs Linux CLI

Cockpit provides a convenient **web GUI**, but it does not replace the Linux command line.

For example, you can manage a service through Cockpit's web interface, but the same task can be performed from the terminal:

```bash
systemctl status nginx
systemctl start nginx
systemctl stop nginx
```

Cockpit is especially useful when you want a **visual overview of the server** or need to perform common administration tasks through a browser.

---

## Interview Point

> **Cockpit is a web-based GUI for Linux server administration and monitoring. It allows administrators to manage services, logs, users, storage, networking, and system resources from a browser, but it does not replace the Linux command line.**

---

## Quick Reference

```bash
# Enable and start Cockpit
sudo systemctl enable --now cockpit.socket

# Check status
systemctl status cockpit.socket

# Start
sudo systemctl start cockpit.socket

# Stop
sudo systemctl stop cockpit.socket

# Restart
sudo systemctl restart cockpit.socket

# Check port 9090
ss -tulpn | grep 9090
```

Access:

```text
https://<server-ip>:9090
```
