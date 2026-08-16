## What is SCP Command?

**SCP (Secure Copy)** is a command-line utility used to securely transfer files and directories between local and remote systems over **SSH (Secure Shell)**.

SCP encrypts the data during transfer because it uses SSH for communication. It is commonly used as a simple alternative to traditional unencrypted file-transfer methods such as FTP.

---

## Why Use SCP?

SCP is commonly used by **Linux administrators, DevOps engineers, and cloud engineers** to quickly transfer files between systems.

### Common Use Cases

- Upload application files to a server
- Download log files from a remote server
- Transfer backup files
- Copy configuration files
- Transfer scripts
- Copy files between Linux servers
- Transfer deployment artifacts
- Upload files to cloud servers

---

## SCP Syntax

```bash
scp [options] source destination
```

The basic structure is:

```text
scp → Source → Destination
```

---

## Copy Local File to Remote Server

```bash
scp file.txt ubuntu@192.170.1.20:/home/ubuntu/
```

This uploads `file.txt` from the local machine to `/home/ubuntu/` on the remote server.

```text
Local Machine
     │
     │ SCP / SSH
     ▼
Remote Server
```

---

## Copy Remote File to Local Machine

```bash
scp ubuntu@192.170.1.20:/home/ubuntu/file.txt .
```

The `.` represents the **current local directory**.

This downloads `file.txt` from the remote server to the current directory.

---

## Copy an Entire Directory

Use the **`-r`** option to recursively copy directories.

```bash
scp -r project/ ubuntu@192.170.1.20:/home/ubuntu/
```

This copies the entire `project` directory and its contents to the remote server.

---

## Copy File Using SSH Private Key

Cloud providers such as AWS commonly use SSH key authentication.

Use the **`-i`** option to specify the private key:

```bash
scp -i my-key.pem app.zip ubuntu@13.201.10.20:/home/ubuntu/
```

Example with an EC2 server:

```bash
scp -i my-key.pem application.tar.gz ubuntu@54.123.45.67:/home/ubuntu/
```

Make sure the private key has appropriate permissions when required:

```bash
chmod 400 my-key.pem
```

---

## Copy File Between Two Remote Linux Servers

SCP can be used to transfer files between remote systems.

```bash
scp user1@server1:/home/user1/file.txt user2@server2:/home/user2/
```

The file is copied from **server1** to **server2**.

---

## Copy File from Remote Server to Another Remote Server

You can also specify SSH keys and ports when required:

```bash
scp -i key.pem user1@server1:/home/user1/file.txt user2@server2:/home/user2/
```

The exact authentication requirements depend on the SSH configuration of both servers.

---

## Common SCP Options

| Option | Description                                |
| ------ | ------------------------------------------ |
| `-r`   | Copy directories recursively               |
| `-i`   | Specify SSH private key                    |
| `-P`   | Specify SSH port                           |
| `-p`   | Preserve file timestamps and permissions   |
| `-C`   | Compress data during transfer              |
| `-v`   | Display verbose output for troubleshooting |

> **Note:** SCP uses uppercase `-P` for specifying the SSH port.

---

## Example with Custom SSH Port

If the SSH server uses port `2222` instead of the default port `22`:

```bash
scp -P 2222 file.txt ubuntu@192.168.1.10:/home/ubuntu/
```

---

## Example: Upload Directory with SSH Key and Custom Port

```bash
scp -i my-key.pem -P 2222 -r project/ ubuntu@192.168.1.10:/home/ubuntu/
```

This command:

- `-i my-key.pem` → Uses the SSH private key
- `-P 2222` → Uses SSH port `2222`
- `-r` → Copies the directory recursively
- `project/` → Source directory
- `/home/ubuntu/` → Remote destination

---

## How SCP Works

```text
Local Machine
      │
      │
      │ SCP
      │
      ▼
   SSH Connection
      │
      │ Encrypted Transfer
      ▼
Remote Linux Server
```

The general process is:

1. SCP starts an SSH connection.
2. The client authenticates with the remote server.
3. SSH establishes an encrypted connection.
4. SCP transfers the file or directory.
5. The remote system stores the transferred data at the specified destination.

---

## SCP with AWS EC2

SCP is frequently used with AWS EC2 instances to upload application files, scripts, configuration files, and deployment packages.

Example:

```bash
scp -i my-key.pem app.zip ubuntu@EC2_PUBLIC_IP:/home/ubuntu/
```

For Amazon Linux:

```bash
scp -i my-key.pem app.zip ec2-user@EC2_PUBLIC_IP:/home/ec2-user/
```

---

## Advantages of SCP

- Secure file transfer using SSH
- Encrypted communication
- Simple command-line syntax
- No separate file-transfer server required
- Supports files and directories
- Supports SSH key authentication
- Available on most Linux and Unix systems
- Useful for automation and deployment scripts

---

## SCP vs WinSCP

| SCP                                | WinSCP                               |
| ---------------------------------- | ------------------------------------ |
| Command-line utility               | Graphical application                |
| Commonly used from Linux terminals | Commonly used on Windows             |
| No graphical interface             | Drag-and-drop interface              |
| Good for scripts and automation    | Good for manual file management      |
| Fast for terminal users            | Beginner-friendly                    |
| Uses SSH                           | Supports SFTP, SCP, FTP, WebDAV      |
| Ideal for DevOps automation        | Ideal for interactive administration |

---

## SCP vs SFTP

| Feature                      | SCP       | SFTP           |
| ---------------------------- | --------- | -------------- |
| Secure                       | Yes       | Yes            |
| Uses SSH                     | Yes       | Yes            |
| File transfer                | Yes       | Yes            |
| Interactive file management  | Limited   | Yes            |
| Resume interrupted transfers | Limited   | Better support |
| Automation                   | Excellent | Excellent      |
| Simple one-time copy         | Excellent | Good           |

For simple file copying, **SCP is convenient**. For interactive file management and more advanced transfer capabilities, **SFTP is generally preferred**.

---

## When to Use SCP

Use **SCP** when you need a quick and secure way to transfer files or directories between systems.

Common scenarios include:

- Application deployment
- Uploading scripts
- Downloading logs
- Transferring backups
- Copying configuration files
- Uploading files to AWS EC2
- Moving files between Linux servers

For more advanced file synchronization, tools such as **`rsync`** are often more suitable.
