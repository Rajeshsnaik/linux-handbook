## Oracle VirtualBox Setup on Windows

Oracle VirtualBox is a free virtualization software that allows you to run multiple operating systems on a Windows computer.

It creates **Virtual Machines (VMs)** where you can install Linux, Windows, and other operating systems without affecting the main Windows system.

### Common Uses of VirtualBox

- Learning Linux
- Testing operating systems
- Software development
- Server administration practice
- Testing network configurations
- Practicing DevOps tools

---

## Installing Linux CentOS on VirtualBox

To install CentOS on VirtualBox:

1. Open **VirtualBox**.
2. Click **New** to create a virtual machine.
3. Enter a name for the VM.
4. Select the appropriate Linux type and version.
5. Allocate **RAM** to the VM.
6. Allocate **CPU cores**.
7. Create a virtual hard disk.
8. Attach the **CentOS ISO** file to the VM.
9. Start the VM.
10. Follow the CentOS installation wizard.
11. Configure the language, keyboard, storage, network, and timezone.
12. Create a user account and password.
13. Complete the installation and reboot the VM.

After installation, CentOS can be used as a Linux server for practicing Linux administration and DevOps concepts.

---

## Installing Linux Ubuntu on VirtualBox

To install Ubuntu on VirtualBox:

1. Open **VirtualBox**.
2. Click **New**.
3. Enter the VM name.
4. Select Linux as the operating system.
5. Allocate **RAM** and **CPU**.
6. Create a virtual hard disk.
7. Mount the **Ubuntu ISO** image.
8. Start the VM.
9. Follow the Ubuntu installation wizard.
10. Select the language and keyboard layout.
11. Configure the timezone.
12. Create a username and password.
13. Complete the installation.
14. Restart the VM after installation.

Ubuntu can then be used for Linux administration, scripting, networking, Docker, and other DevOps practices.

---

# Access Linux Server Remotely Using SSH

**SSH (Secure Shell)** is a network protocol used to securely access and manage remote Linux systems.

Instead of physically accessing the Linux machine, you can connect to it remotely using an SSH client.

```text
Windows Computer
       │
       │ SSH
       ▼
Linux Server
```

---

## What is PuTTY Terminal?

**PuTTY** is a free SSH client for Windows that allows you to securely connect to remote Linux servers.

It supports protocols such as:

- SSH
- Telnet
- Serial
- Rlogin

For Linux server administration, **SSH** is the most commonly used protocol.

---

## Installing PuTTY

To install PuTTY on Windows:

1. Download and install PuTTY.
2. Open **PuTTY**.
3. Enter the Linux server's IP address.
4. Set the connection type to **SSH**.
5. Use port **22** unless your SSH server uses a different port.
6. Click **Open**.
7. Enter your Linux username.
8. Authenticate using a password or SSH key.

---

## Access Linux CentOS Using PuTTY

To connect to a CentOS server:

1. Start the CentOS VM.
2. Find the server's IP address.

```bash
ip addr
```

3. Open PuTTY on Windows.
4. Enter the CentOS IP address.
5. Select **SSH**.
6. Connect to the server.
7. Enter the CentOS username.
8. Enter the password or authenticate using an SSH key.

Once authenticated, you can manage the CentOS server remotely.

---

## Access Ubuntu Using PuTTY

To connect to an Ubuntu server:

1. Start the Ubuntu VM.
2. Find its IP address.

```bash
ip addr
```

3. Open PuTTY.
4. Enter the Ubuntu server IP address.
5. Select **SSH**.
6. Connect to the server.
7. Enter the Ubuntu username.
8. Authenticate using the password or SSH key.

You can then execute Linux commands remotely.

---

## Access Linux Server Using Windows CMD with SSH

Modern versions of Windows include the **OpenSSH client**, allowing you to connect to Linux servers directly from Command Prompt or PowerShell.

```bash
ssh username@server-ip
```

Example:

```bash
ssh rajesh@192.170.1.20
```

If SSH is running on a different port:

```bash
ssh -p 2222 username@server-ip
```

---

## Access Linux Server Using Git Bash with SSH

**Git Bash** provides a Linux-like terminal environment on Windows and includes SSH support.

You can use the same SSH command:

```bash
ssh username@server-ip
```

Example:

```bash
ssh rajesh@192.170.1.20
```

Git Bash is useful for developers and DevOps engineers because it provides common Unix commands along with Git and SSH.

---

## Introducing MobaXterm Multi-tab Terminal

**MobaXterm** is an advanced terminal application for Windows that combines several remote administration tools in a single application.

### Features

- SSH
- SFTP
- Multiple terminal tabs
- X11 forwarding
- Remote file management
- Port forwarding
- Unix/Linux commands
- Session management

MobaXterm is useful for **Linux administrators, DevOps engineers, and cloud engineers** who need to manage multiple remote servers.

```text
MobaXterm
    │
    ├── SSH → Linux Server 1
    │
    ├── SSH → Linux Server 2
    │
    ├── SSH → Linux Server 3
    │
    └── SFTP → Remote Files
```

---

## SSH Authentication Methods

SSH commonly uses two authentication methods:

### Password Authentication

The user provides a username and password.

```bash
ssh username@server-ip
```

### SSH Key Authentication

SSH keys provide a more secure way to authenticate without entering a password every time.

The basic concept is:

```text
Client
  │
  ├── Private Key
  │
  ▼
SSH Server
  │
  └── Public Key
```

The **private key** should remain securely stored on the client machine and should never be shared.

---

## Common SSH Tools on Windows

| Tool             | SSH Support | SFTP | Multi-tab | Best Use                  |
| ---------------- | ----------- | ---- | --------- | ------------------------- |
| PuTTY            | Yes         | Yes  | Limited   | Simple SSH connections    |
| CMD / PowerShell | Yes         | No   | No        | Quick SSH access          |
| Git Bash         | Yes         | No   | No        | Developers and DevOps     |
| MobaXterm        | Yes         | Yes  | Yes       | Managing multiple servers |

---

## Summary

VirtualBox allows you to create Linux virtual machines on a Windows computer for learning and testing.

Once Linux is installed, SSH allows you to manage the Linux server remotely.

Common Windows SSH tools include:

- **PuTTY**
- **CMD / PowerShell**
- **Git Bash**
- **MobaXterm**

These tools are useful for practicing **Linux administration, networking, cloud computing, and DevOps** without requiring a separate physical Linux machine.
