# Day 7 — Disk, Storage & Permissions

> **Linux & DevOps Learning Journey — Day 7**

![Disk, Storage & Permissions](./Day%207.png)

Today we covered essential **Linux disk, storage, and permission concepts** used to monitor disk usage, manage storage, control file ownership, configure access permissions, and secure shared directories and files.

---

## What We Covered Today

| Topic                                     | GitHub Repository                                       | What We Covered                                                                                                                                                                                      |
| ----------------------------------------- | ------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Disk Space Monitoring**                 | [`Disk Space Monitoring`](./Disk%20Space%20Monitoring/) | Monitoring filesystem and disk usage using commands such as `df`, `du`, `lsblk`, and checking disk space, inode usage, large files, and storage consumption.                                         |
| **LVM**                                   | [`LVM`](./LVM/)                                         | Understanding Logical Volume Manager, including Physical Volumes (PV), Volume Groups (VG), Logical Volumes (LV), creating and extending storage, adding disks, and LVM snapshots.                    |
| **ACL**                                   | [`ACL`](./ACL/)                                         | Managing fine-grained file and directory permissions for specific users and groups using `getfacl` and `setfacl`.                                                                                    |
| **`umask`**                               | [`umask`](./umask/)                                     | Understanding default file and directory permissions and how `umask` controls which permissions are removed during file and directory creation.                                                      |
| **`chown`**                               | [`chown`](./chown/)                                     | Changing file and directory ownership, including user ownership, group ownership, recursive ownership, and verifying ownership with `ls` and `stat`.                                                 |
| **`chgrp`**                               | [`chgrp`](./chgrp/)                                     | Changing the group ownership of files and directories, including recursive group changes and group management for shared directories.                                                                |
| **SUID & SGID**                           | [`SUID & SGID`](./SGID%20&%20SUID/)                     | Understanding special Linux permissions, how SUID provides executable files with the owner's effective privileges, and how SGID provides group-based execution and group inheritance on directories. |
| **Sticky Bit / Restricted Deletion Flag** | [`Sticky Bit`](./Sticky%20Bit/)                         | Understanding the Sticky Bit for shared directories and how it restricts users from deleting or renaming files owned by other users.                                                                 |

---

## Key Takeaways

By the end of Day 7, we understood:

- How to monitor **disk space and filesystem usage** using `df`, `du`, and `lsblk`.

- How to identify **large files, directories, and inode usage** during disk-space troubleshooting.

- The fundamentals of **LVM**, including **Physical Volume (PV), Volume Group (VG), and Logical Volume (LV)**.

- How LVM provides **flexible storage management** and allows logical volumes to be extended when additional disk space is available.

- How **ACL** provides fine-grained permissions for specific users and groups beyond traditional Linux `rwx` permissions.

- How **`umask`** controls default permissions for newly created files and directories.

- How to manage file ownership using **`chown`** and group ownership using **`chgrp`**.

- The difference between **ownership and permissions**, and how `chown`, `chgrp`, `chmod`, and ACL work together.

- How **SUID** allows an executable to run with the file owner's effective privileges.

- How **SGID** provides group-based execution on files and group inheritance on directories.

- How the **Sticky Bit** protects files in shared directories by restricting deletion and renaming.

- How these concepts are useful for **Linux administration, storage management, security, troubleshooting, shared environments, and DevOps tasks**.

---

## Follow More

Follow my **Linux & DevOps learning journey** as I continue covering Linux, Networking, Git, Docker, Kubernetes, AWS, Terraform, CI/CD, and other DevOps technologies.

⭐ **Star the repository** if you find these notes useful.

**GitHub Profile:** [GitHub](https://github.com/Rajeshsnaik)

**LinkedIn:** [LinkedIn](https://www.linkedin.com/in/rajeshnaik2002/)
