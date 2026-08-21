# Linux LVM — Logical Volume Manager

**LVM (Logical Volume Manager)** is a Linux storage management system that allows you to manage disk space more flexibly than traditional disk partitions.

With LVM, you can:

- Create logical volumes
- Extend volumes when more space is required
- Reduce volumes when supported and done safely
- Combine multiple disks into a storage pool
- Create snapshots
- Manage storage without depending entirely on fixed partitions

---

## LVM Architecture

LVM has three main components:

```text
Physical Disk
     ↓
Physical Volume (PV)
     ↓
Volume Group (VG)
     ↓
Logical Volume (LV)
     ↓
Filesystem
     ↓
Mount Point
```

### Example

```text
/dev/sdb
   ↓
Physical Volume
   ↓
Volume Group: vg_data
   ↓
Logical Volume: lv_app
   ↓
ext4 filesystem
   ↓
/app
```

---

# 1. Physical Volume (PV)

A **Physical Volume** is a disk or disk partition initialized for use by LVM.

Examples:

```bash
pvcreate /dev/sdb
```

Or:

```bash
pvcreate /dev/sdb1
```

---

## Check Physical Volumes

```bash
pvs
```

Detailed information:

```bash
pvdisplay
```

Example:

```text
PV         VG       Fmt  Attr PSize   PFree
/dev/sdb   vg_data  lvm2 a--  <20.00g  20.00g
```

---

# 2. Volume Group (VG)

A **Volume Group** is a storage pool created from one or more Physical Volumes.

Create a volume group:

```bash
vgcreate vg_data /dev/sdb
```

Check:

```bash
vgs
```

Detailed information:

```bash
vgdisplay
```

Example:

```text
VG       #PV  #LV  VSize   VFree
vg_data   1    0   <20.00g  <20.00g
```

---

# 3. Logical Volume (LV)

A **Logical Volume** is the storage volume created inside a Volume Group.

Create a 10 GB logical volume:

```bash
lvcreate -L 10G -n lv_app vg_data
```

Check:

```bash
lvs
```

Detailed information:

```bash
lvdisplay
```

Example:

```text
LV      VG       Attr       LSize
lv_app  vg_data  -wi-a----- 10.00g
```

---

# Create a Complete LVM Setup

Suppose you have a new disk:

```text
/dev/sdb
```

### Step 1 — Create Physical Volume

```bash
pvcreate /dev/sdb
```

### Step 2 — Create Volume Group

```bash
vgcreate vg_data /dev/sdb
```

### Step 3 — Create Logical Volume

```bash
lvcreate -L 10G -n lv_app vg_data
```

### Step 4 — Create Filesystem

For `ext4`:

```bash
mkfs.ext4 /dev/vg_data/lv_app
```

### Step 5 — Create Mount Point

```bash
mkdir /app
```

### Step 6 — Mount the Logical Volume

```bash
mount /dev/vg_data/lv_app /app
```

### Step 7 — Verify

```bash
df -h
```

You should see something similar to:

```text
Filesystem                    Size  Used Avail Use% Mounted on
/dev/mapper/vg_data-lv_app     10G   24M  9.5G   1% /app
```

---

# Extend an LVM Volume

One of the major advantages of LVM is that you can increase storage when required.

Suppose:

```text
/app = 10G
```

and you want to increase it to:

```text
/app = 15G
```

---

## Step 1 — Check Free Space

```bash
vgs
```

or:

```bash
vgdisplay
```

Make sure the Volume Group has enough free space.

---

## Step 2 — Extend the Logical Volume

```bash
lvextend -L +5G /dev/vg_data/lv_app
```

Or:

```bash
lvextend -L 15G /dev/vg_data/lv_app
```

---

## Step 3 — Extend the Filesystem

For `ext4`:

```bash
resize2fs /dev/vg_data/lv_app
```

For XFS:

```bash
xfs_growfs /app
```

### Easier Method

You can often resize the LV and filesystem together:

```bash
lvextend -r -L +5G /dev/vg_data/lv_app
```

`-r` automatically resizes the filesystem when supported.

---

# Add a New Disk to LVM

Suppose the existing Volume Group is:

```text
vg_data
```

and you add another disk:

```text
/dev/sdc
```

### Step 1 — Create PV

```bash
pvcreate /dev/sdc
```

### Step 2 — Add PV to VG

```bash
vgextend vg_data /dev/sdc
```

Check:

```bash
vgs
```

Now the Volume Group has additional storage.

---

# Reduce an LVM Volume

Reducing a logical volume is **dangerous** if done incorrectly.

You must reduce the filesystem **before** reducing the LV.

For example, with an `ext4` filesystem:

```bash
umount /app
```

Check the filesystem:

```bash
e2fsck -f /dev/vg_data/lv_app
```

Resize the filesystem:

```bash
resize2fs /dev/vg_data/lv_app 8G
```

Then reduce the LV:

```bash
lvreduce -L 8G /dev/vg_data/lv_app
```

Mount again:

```bash
mount /dev/vg_data/lv_app /app
```

> **Important:** Never reduce an LV first and resize the filesystem afterward. You can cause data loss.

XFS filesystems generally **cannot be reduced in place**. A backup/recreate/restore approach is normally required.

---

# LVM Snapshots

LVM can create snapshots of logical volumes.

Example:

```bash
lvcreate -L 2G -s -n lv_app_snapshot /dev/vg_data/lv_app
```

Check:

```bash
lvs
```

Snapshots are commonly used for:

- Backup workflows
- Testing
- Temporary recovery points
- Consistent copies before certain operations

> **Important:** An LVM snapshot is not a replacement for a proper backup. If the underlying storage is lost, the snapshot is lost too.

---

# Remove LVM Components

### Remove Logical Volume

```bash
lvremove /dev/vg_data/lv_app
```

### Remove Volume Group

```bash
vgremove vg_data
```

### Remove Physical Volume

```bash
pvremove /dev/sdb
```

> **Warning:** These commands can permanently destroy data. Always verify the device and volume before running them.

---

# Important LVM Commands

## Physical Volume

```bash
pvcreate /dev/sdb
pvs
pvdisplay
pvremove /dev/sdb
```

## Volume Group

```bash
vgcreate vg_data /dev/sdb
vgs
vgdisplay
vgextend vg_data /dev/sdc
vgremove vg_data
```

## Logical Volume

```bash
lvcreate -L 10G -n lv_app vg_data
lvs
lvdisplay
lvextend -L +5G /dev/vg_data/lv_app
lvextend -r -L +5G /dev/vg_data/lv_app
lvreduce -L 8G /dev/vg_data/lv_app
lvremove /dev/vg_data/lv_app
```

---

# Useful LVM Commands

```bash
lsblk                         # View disks and partitions
pvs                           # Physical volumes
vgs                           # Volume groups
lvs                           # Logical volumes

pvdisplay                     # Detailed PV information
vgdisplay                     # Detailed VG information
lvdisplay                     # Detailed LV information

df -h                         # Filesystem usage
blkid                         # Filesystem/UUID information
```

---

# LVM vs Traditional Partitioning

| Traditional Partitioning                        | LVM                          |
| ----------------------------------------------- | ---------------------------- |
| Fixed partitions                                | Flexible logical volumes     |
| Resizing can be difficult                       | Easier to extend             |
| Usually tied directly to disk partitions        | Uses storage pools           |
| Limited flexibility                             | Highly flexible              |
| No built-in snapshot feature                    | Supports snapshots           |
| Multiple disks require additional configuration | Multiple PVs can form one VG |

---

# Real-World Example

Suppose a Linux server has:

```text
/dev/sdb = 100 GB
/dev/sdc = 100 GB
```

Create LVM:

```bash
pvcreate /dev/sdb /dev/sdc
```

Create a Volume Group:

```bash
vgcreate vg_app /dev/sdb /dev/sdc
```

Now:

```text
/dev/sdb ──┐
           ├──> vg_app = 200 GB
/dev/sdc ──┘
```

Create a 150 GB Logical Volume:

```bash
lvcreate -L 150G -n lv_data vg_app
```

Create filesystem:

```bash
mkfs.ext4 /dev/vg_app/lv_data
```

Mount:

```bash
mkdir /data
mount /dev/vg_app/lv_data /data
```

You now have:

```text
/dev/sdb (100G) ──┐
                  │
                  ├──> vg_app (200G)
                  │        │
/dev/sdc (100G) ──┘        ↓
                       lv_data (150G)
                            ↓
                          ext4
                            ↓
                          /data
```

The remaining **50 GB** stays available inside the Volume Group and can later be assigned to another Logical Volume or used to extend an existing one.

---

# Quick Reference

```bash
# Physical Volume
pvcreate /dev/sdb
pvs
pvdisplay

# Volume Group
vgcreate vg_data /dev/sdb
vgs
vgdisplay
vgextend vg_data /dev/sdc

# Logical Volume
lvcreate -L 10G -n lv_app vg_data
lvs
lvdisplay

# Filesystem
mkfs.ext4 /dev/vg_data/lv_app

# Mount
mkdir /app
mount /dev/vg_data/lv_app /app

# Extend
lvextend -r -L +5G /dev/vg_data/lv_app

# Snapshot
lvcreate -L 2G -s -n lv_app_snapshot /dev/vg_data/lv_app

# Remove
lvremove /dev/vg_data/lv_app
vgremove vg_data
pvremove /dev/sdb
```

> **Interview Point:** LVM provides a flexible storage layer between physical disks and filesystems. **PV → VG → LV → Filesystem → Mount Point** is the core LVM architecture.
