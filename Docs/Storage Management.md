# Storage Management

## What is Storage Management?

Storage Management is the process of organizing, managing, and maintaining disks, partitions, volumes, and file systems. It helps store data efficiently and ensures that files are available when needed.

---

# Types of Storage

Storage is mainly divided into two types:

- Primary Storage
- Secondary Storage

---

# Primary Storage

Primary storage is directly accessed by the CPU. It is very fast but has limited capacity.

### RAM (Random Access Memory)

RAM is temporary memory that stores data while the computer is running. The data is lost when the system is turned off.

**Example:** DDR4, DDR5 RAM

### ROM (Read Only Memory)

ROM stores permanent instructions used to start the computer. The data remains even after the system is powered off.

**Example:** BIOS, UEFI Firmware

---

# Dynamic RAM (DRAM)

Dynamic RAM is the most common type of RAM used in computers. It stores data temporarily and needs to refresh continuously to keep the data.

**Example:** DDR3, DDR4, DDR5 Memory

---

# Secondary Storage

Secondary storage is used to permanently store files, applications, and the operating system.

---

## Magnetic Storage Device

These devices store data using magnetic technology.

**Examples:**

- Hard Disk Drive (HDD)
- Magnetic Tape

**Advantages**

- Large storage capacity
- Low cost

**Limitations**

- Slower than SSD
- Contains moving parts

---

## Optical Storage Device

These devices use a laser to read and write data.

**Examples**

- CD
- DVD
- Blu-ray Disc

**Advantages**

- Easy to carry
- Good for backups

**Limitations**

- Limited storage
- Slower than HDD and SSD

---

## Flash Storage Device

Flash storage uses memory chips and has no moving parts.

**Examples**

- SSD
- USB Flash Drive
- Memory Card

**Advantages**

- High speed
- Durable
- Lightweight

**Limitations**

- More expensive than HDD

---

# Types of Disks

### HDD (Hard Disk Drive)

Uses magnetic disks to store data. It offers high storage capacity at a lower cost but is slower than SSD.

### SSD (Solid State Drive)

Uses flash memory instead of moving parts. It provides faster boot time and better performance.

### NVMe SSD

A high-speed SSD that connects through the PCIe interface and offers much better performance than a SATA SSD.

---

# File Systems

## FAT (File Allocation Table)

FAT is one of the oldest file systems and is mainly used for USB drives and memory cards.

**Features**

- Simple and widely supported
- Works with many operating systems

**Limitations**

- Limited file size
- No security permissions
- No encryption

---

## NTFS (New Technology File System)

NTFS is the default file system used in Windows.

**Features**

- Supports large files
- File and folder permissions
- Encryption (EFS)
- Compression
- Disk quotas
- Better security
- Journaling for recovery

**Limitations**

- Limited support on some non-Windows operating systems

---

## ReFS (Resilient File System)

ReFS is designed for large storage systems and enterprise environments.

**Features**

- Improved data integrity
- Automatic error detection
- Better protection against data corruption
- Supports very large volumes

**Limitations**

- Cannot be used as a boot drive in most Windows editions
- Does not support some NTFS features

---

# Types of Partitions

## Primary Partition

A Primary Partition can store the operating system and can be marked as an active partition for booting.

---

## Extended Partition

An Extended Partition is used to create multiple logical drives. It cannot store files directly but acts as a container for logical partitions.

---

# Types of Storage Connection

## DAS (Direct Attached Storage)

Storage directly connected to one computer.

**Examples**

- Internal HDD
- External USB Drive

---

## NAS (Network Attached Storage)

A storage device connected to a network that allows multiple users to access shared files.

**Example**

Office File Server

---

## SAN (Storage Area Network)

A high-speed storage network used in enterprise environments to connect servers with shared storage.

**Example**

Enterprise Data Centers

---

# Disk Management

Disk Management is a Windows tool used to manage disks, partitions, and volumes.

### Shortcut Command

```cmd
diskmgmt.msc
```

---

# Shrinking a Volume

To reduce the size of an existing partition:

1. Open **Disk Management**.
2. Right-click the required volume.
3. Select **Shrink Volume**.
4. Enter the amount of space to shrink.
5. Click **Shrink**.

The remaining space becomes **Unallocated Space**.

---

# Creating a New Simple Volume

After shrinking a partition, a new volume can be created.

### Steps

1. Right-click the **Unallocated Space**.
2. Select **New Simple Volume**.
3. Click **Next**.
4. Enter the volume size.
5. Assign a drive letter.
6. Select the file system (NTFS is recommended).
7. Give the volume a name.
8. Click **Finish**.

The new drive will now appear in File Explorer.

---

# Permissions

Windows provides two main types of permissions.

## Share Permissions

Share permissions control access when a folder is shared over the network.

Common permissions:

- Read
- Change
- Full Control

---

## NTFS Permissions

NTFS permissions control access to files and folders stored on an NTFS partition.

Common permissions:

- Full Control
- Modify
- Read & Execute
- List Folder Contents
- Read
- Write

NTFS permissions provide more detailed security and are commonly used in enterprise environments.
````
