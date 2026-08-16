# WinSCP Setup

**WinSCP (Windows Secure Copy)** is a Windows file-transfer client used to securely transfer files between a Windows computer and a remote Linux server.

It supports **SFTP, SCP, FTP, and WebDAV**. **SFTP over SSH** is the recommended option.

---

## Why Use WinSCP?

WinSCP provides a graphical interface for managing Linux server files without relying entirely on terminal commands.

**Common Uses:**

- Upload application files
- Download server logs
- Edit configuration files
- Transfer backups
- Upload Docker Compose files
- Manage files and directories
- Change Linux file permissions

---

## Connect to a Linux Server

Use these details in WinSCP:

| Setting       | Example                        |
| ------------- | ------------------------------ |
| File Protocol | SFTP                           |
| Host Name     | Server IP / Domain             |
| Port          | `22`                           |
| Username      | `ubuntu`, `ec2-user`, `centos` |
| Password      | Server password / SSH key      |

For AWS EC2, SSH key authentication is commonly used.

---

## Using SSH Private Key

Go to:

```text
Advanced
   ↓
SSH
   ↓
Authentication
   ↓
Private Key
```

Select your SSH private key file.

For example:

```text
my-server.pem
```

If WinSCP asks to convert the key to its supported format, allow it to convert the `.pem` file to `.ppk`.

---

## AWS EC2 Example

Suppose your EC2 instance has:

```text
Public IP: 13.234.56.78
Username: ubuntu
Port: 22
Private Key: my-server.pem
```

Configure WinSCP as:

```text
File Protocol: SFTP
Host Name: 13.234.56.78
Port Number: 22
User Name: ubuntu
Private Key File: my-server.ppk
```

Click **Login**.

---

## File Transfer

After connecting, WinSCP displays two panels:

```text
Left Side                    Right Side
------------------------------------------------
Windows Computer             Linux Server

C:\Users\Rajesh\             /home/ubuntu/
project/                     project/
files/                       files/
```

You can **drag and drop** files between the two panels.

### Upload

```text
Windows → Linux Server
```

Example:

```text
docker-compose.yml
```

can be uploaded to:

```text
/home/ubuntu/
```

### Download

```text
Linux Server → Windows
```

For example, download:

```text
/var/log/nginx/access.log
```

to your Windows computer for analysis.

---

## Editing Linux Files

WinSCP allows you to right-click a file and select:

```text
Edit
```

For example:

```text
/etc/nginx/nginx.conf
```

You can edit the file locally and WinSCP can upload the modified version back to the server.

> **Note:** System files such as `/etc/nginx/nginx.conf` may require `sudo` privileges. WinSCP's normal SFTP session does not automatically give you root access.

---

## Linux File Permissions

WinSCP can also modify file permissions.

Right-click a file:

```text
File
   ↓
Properties
   ↓
Permissions
```

Linux permissions might look like:

```text
-rwxr-xr-x
```

Equivalent numeric permission:

```text
755
```

For example:

```bash
chmod 755 script.sh
```

---

## Important Linux Directories

When managing a Linux server through WinSCP, commonly used directories include:

| Directory         | Purpose                       |
| ----------------- | ----------------------------- |
| `/home/ubuntu/`   | Ubuntu user's files           |
| `/var/www/`       | Web application files         |
| `/etc/nginx/`     | Nginx configuration           |
| `/var/log/`       | System and application logs   |
| `/tmp/`           | Temporary files               |
| `/opt/`           | Optional application software |
| `/usr/local/bin/` | Custom executable programs    |

---

## WinSCP with AWS EC2

Typical workflow:

```text
Windows Computer
       |
       | SFTP over SSH
       | Port 22
       ↓
AWS EC2 Instance
       |
       ├── /home/ubuntu/
       ├── /var/www/
       ├── /etc/nginx/
       └── /var/log/
```

The EC2 **Security Group** must allow SSH traffic:

```text
Type: SSH
Protocol: TCP
Port: 22
Source: Your IP Address
```

For better security, avoid allowing SSH from:

```text
0.0.0.0/0
```

when it is not necessary.

---

## Common WinSCP Errors

### 1. Connection Refused

Check whether SSH is running:

```bash
sudo systemctl status ssh
```

Also verify that port `22` is allowed in the EC2 Security Group.

---

### 2. Permission Denied

Check the file permissions:

```bash
ls -l filename
```

Check the current user:

```bash
whoami
```

If the file belongs to another user, you may need to change ownership or permissions using SSH.

Example:

```bash
sudo chown ubuntu:ubuntu filename
```

---

### 3. Authentication Failed

Check:

- Username
- Private key
- EC2 instance status
- Security Group
- SSH port
- Correct key pair

For Ubuntu EC2 instances, the username is usually:

```text
ubuntu
```

For Amazon Linux:

```text
ec2-user
```

---

## WinSCP vs SCP Command

### WinSCP

GUI-based:

```text
Windows → WinSCP → Linux Server
```

Useful for:

- Beginners
- Manual file management
- Drag-and-drop transfers
- Browsing server directories

### SCP

Command-line based:

```bash
scp -i my-server.pem app.zip ubuntu@13.234.56.78:/home/ubuntu/
```

Useful for:

- Automation
- Scripts
- Terminal-based workflows
- CI/CD pipelines

---

## Best Practices

- Prefer **SFTP** over plain FTP.
- Use SSH keys instead of passwords where possible.
- Restrict port `22` to trusted IP addresses.
- Never share your private key.
- Keep private keys secure.
- Avoid modifying system configuration files without a backup.
- Use `sudo` carefully.
- Verify file ownership and permissions after uploading files.

---

## Quick Summary

```text
WinSCP
  ↓
SFTP
  ↓
SSH
  ↓
Port 22
  ↓
Linux Server / AWS EC2
```

WinSCP is mainly useful when you want an easy **GUI-based way to transfer and manage files on a remote Linux server**, while SSH/SCP is better suited for command-line operations and automation.
