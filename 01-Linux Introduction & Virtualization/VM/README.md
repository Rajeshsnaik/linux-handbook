## Virtual Machines (VMs)

Virtual Machines (VMs) allow multiple operating systems to run on a single physical server. They are widely used for:

- Server consolidation
- Software testing
- Development environments
- Cloud computing
- Disaster recovery
- Running legacy applications

---

## How Virtualization Works

Virtualization creates virtual versions of physical resources such as CPU, memory, storage, and networking.

A **hypervisor** sits between the hardware and virtual machines, allowing multiple VMs to securely share the same physical server.

---

## What is Hypervisor?

A **hypervisor**, also called a **Virtual Machine Monitor (VMM)**, is software that creates, manages, and runs virtual machines.

It allocates physical hardware resources such as CPU, RAM, storage, and networking to each VM while keeping the VMs isolated from one another.

---

## How Hypervisor Works?

The hypervisor communicates with the physical hardware and distributes resources among multiple virtual machines.

Each VM operates independently with its own:

- Operating system
- Applications
- Virtual CPU
- Virtual memory
- Virtual storage
- Virtual network interface

Although multiple VMs share the same physical server, they remain logically isolated from one another.

---

## Types of Hypervisor

There are two main types of hypervisors:

- **Type 1 (Bare Metal)** – Runs directly on the physical hardware.
- **Type 2 (Hosted)** – Runs on top of an existing operating system.

---

## Type 1 Bare Metal Hypervisor

A **Type 1 Hypervisor** is installed directly on the physical server without requiring a traditional host operating system.

It provides better performance, security, and scalability because it interacts directly with the underlying hardware.

Type 1 hypervisors are commonly used in:

- Enterprise data centers
- Cloud platforms
- Production servers
- Large-scale virtualization environments

**Examples:**

- VMware ESXi
- Microsoft Hyper-V
- Xen Hypervisor
- KVM (Kernel-based Virtual Machine)

---

## Type 2 Hosted Hypervisor

A **Type 2 Hypervisor** runs as an application on top of an existing operating system.

The host operating system manages the physical hardware, while the hypervisor manages the virtual machines.

Type 2 hypervisors are commonly used for:

- Local development
- Software testing
- Learning virtualization
- Running another operating system on a personal computer

**Examples:**

- Oracle VirtualBox
- VMware Workstation
- VMware Fusion
- Parallels Desktop

---

## Type 1 vs Type 2 Hypervisor

| Feature     | Type 1                          | Type 2                         |
| ----------- | ------------------------------- | ------------------------------ |
| Runs on     | Physical hardware               | Host operating system          |
| Performance | Higher                          | Lower compared to Type 1       |
| Security    | Generally stronger              | Depends on host OS             |
| Use case    | Enterprise, cloud, data centers | Development, testing, desktop  |
| Examples    | ESXi, Hyper-V, Xen, KVM         | VirtualBox, VMware Workstation |

---

## Simple Virtualization Architecture

```text
              Physical Server
        ┌─────────────────────────┐
        │     CPU / RAM / Disk    │
        │       Networking        │
        └────────────┬────────────┘
                     │
              ┌──────▼──────┐
              │  Hypervisor │
              └──────┬──────┘
                     │
       ┌─────────────┼─────────────┐
       │             │             │
   ┌───▼───┐     ┌───▼───┐     ┌───▼───┐
   │  VM 1 │     │  VM 2 │     │  VM 3 │
   │ Linux │     │ Linux │     │Windows│
   └───────┘     └───────┘     └───────┘
```

---

## Key Benefits of Virtual Machines

- **Resource Utilization** – Multiple VMs can share the same physical hardware.
- **Isolation** – Problems in one VM generally do not directly affect other VMs.
- **Cost Reduction** – Fewer physical servers are required.
- **Scalability** – New VMs can be created quickly.
- **Testing** – Different operating systems and software versions can be tested safely.
- **Disaster Recovery** – VMs can be backed up, replicated, and restored.
- **Legacy Application Support** – Older operating systems and applications can continue running inside VMs.

---

## VM vs Physical Server

| Feature             | Virtual Machine   | Physical Server    |
| ------------------- | ----------------- | ------------------ |
| Hardware            | Shared            | Dedicated          |
| Operating System    | Guest OS          | Directly installed |
| Resource Allocation | Virtual           | Physical           |
| Scalability         | Faster            | Requires hardware  |
| Isolation           | Virtual isolation | Physical isolation |
| Cost                | Lower             | Higher             |
| Provisioning        | Minutes           | Longer             |

---

## Real-World Example

Suppose a company has one powerful physical server.

Instead of purchasing three separate physical servers, they can use a hypervisor to create three VMs:

```text
Physical Server
      │
      ▼
  Hypervisor
      │
      ├── VM 1 → Web Server
      │
      ├── VM 2 → Application Server
      │
      └── VM 3 → Database Server
```

All three VMs use the same physical server while remaining logically isolated.

This is one of the main reasons virtualization is widely used in **data centers and cloud computing**.
