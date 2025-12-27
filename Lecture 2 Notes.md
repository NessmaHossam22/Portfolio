

# 📘 **File System – Structured Notes**

---

## 1️⃣ What is a File System?

A **File System** is a major component of the Operating System that manages how data is:

* **Stored**
* **Organized**
* **Accessed**

on **secondary storage** such as disks and tapes.

---

## 2️⃣ Main Characteristics of Files

| Characteristic    | Explanation                                             |
| ----------------- | ------------------------------------------------------- |
| Long-term Storage | Data remains after shutdown                             |
| Sharable          | Files have names and permissions                        |
| Structured        | Data organized in records, directories, and hierarchies |

---

## 3️⃣ File Structure Hierarchy

| Level    | Description                   |
| -------- | ----------------------------- |
| Field    | Single data element           |
| Record   | Collection of related fields  |
| File     | Collection of related records |
| Database | Collection of related files   |

---

## 4️⃣ Common File Operations

| Operation    | Purpose                     |
| ------------ | --------------------------- |
| Create       | Create new file             |
| Delete       | Remove file                 |
| Open / Close | Allow / stop process access |
| Read / Write | Retrieve or modify data     |

---

## 5️⃣ File Management System Objectives

* Meet user needs
* Ensure data validity
* Optimize performance
* Support multiple devices
* Prevent data loss
* Provide standard I/O interface
* Support multi-user access

---

## 6️⃣ Types of File Organization 

| Method                 | Organization      | How it works                                                                                         | Advantages                     |
| ---------------------- | ----------------- | ---------------------------------------------------------------------------------------------------- | ------------------------------ |
| **Pile (Heap)**        | Unordered         | Records are stored in the order they arrive, with no sorting or indexing.                            | Simple, fast insertion         |
| **Sequential**         | Ordered by key    | Records are stored in sorted order according to a key and accessed sequentially or by binary search. | Efficient for batch processing |
| **Indexed Sequential** | Hybrid            | Data file is stored sequentially and an index provides direct access to records.                     | Flexible access, faster search |
| **Index**              | Key → location    | All records are accessed only through an index table that maps keys to block addresses.              | Very fast lookup               |
| **Hashed**             | Hash(key) → block | Record location is computed using a hash function on its key.                                        | Fastest direct access          |

---

## 7️⃣ File Software Architecture

| Layer                | Function                   |
| -------------------- | -------------------------- |
| User Program         | Requests file operations   |
| Logical I/O          | Handles access methods     |
| Basic I/O Supervisor | Schedules disk operations  |
| Basic File System    | Manages blocks & buffering |
| Device Drivers       | Communicate with hardware  |

---

## 8️⃣ File Directory

### Directory Contains

| Category       | Information                           |
| -------------- | ------------------------------------- |
| Basic          | Name, Type, Organization              |
| Address        | Volume, Start address, Size           |
| Access Control | Owner, Permissions                    |
| Usage          | Creation, Modification, Backup, Usage |

### Directory Operations

Search – Create – Delete – List – Update

---

## 9️⃣ File Sharing & Access Rights

### User Classes

Specific User – Group – All Users

### Permissions **(Comparison)**

| Right             | Meaning          |
| ----------------- | ---------------- |
| None              | No access        |
| Knowledge         | Know file exists |
| Read              | Read data        |
| Write / Update    | Modify data      |
| Append            | Add only         |
| Execute           | Run file         |
| Change Protection | Modify rights    |
| Delete            | Remove file      |

### Simultaneous Access Management

| Method          | Description                 |
| --------------- | --------------------------- |
| Whole File Lock | Simple but restrictive      |
| Partial Lock    | Efficient concurrent access |

---

## 🔟 Record Blocking **(Comparison)**

| Type               | Record Size | Can Split? | Fragmentation |
| ------------------ | ----------- | ---------- | ------------- |
| Fixed Length       | Fixed       | ❌          | Internal      |
| Variable Spanned   | Variable    | ✔          | None          |
| Variable Unspanned | Variable    | ❌          | Internal      |

---

## 1️⃣1️⃣ File Allocation **(Comparison)**

| Method     | Storage Style     | Advantages                | Disadvantages                       |
| ---------- | ----------------- | ------------------------- | ----------------------------------- |
| Contiguous | Continuous blocks | Fast access               | External fragmentation, hard growth |
| Chained    | Linked blocks     | No external fragmentation | Slow random access                  |
| Indexed    | Index table       | Fast, flexible            | Extra index space                   |

---

## 1️⃣2️⃣ Free Space Management **(Comparison)**

| Method          | Description         | Advantages             | Disadvantages              |
| --------------- | ------------------- | ---------------------- | -------------------------- |
| Bitmap          | Bit per block       | Fast search            | Needs memory               |
| Chained Free    | Linked free blocks  | Saves space            | Slow search                |
| Indexed Free    | Table of free areas | Fast contiguous search | Extra space                |
| Free Block List | List of free blocks | Simple                 | Inefficient on large disks |

---

## 1️⃣3️⃣ Reliability Mechanisms

| Mechanism        | Purpose                     |
| ---------------- | --------------------------- |
| Locking          | Prevent conflicts           |
| Journaling       | Recover from crash using log file       |
| Batch Allocation | Better performance & safety |

---

## 1️⃣4️⃣ File System Security

| Component             | Function                      |
| --------------------- | ----------------------------- |
| Authentication        | Verify identity               |
| Access Control        | Enforce permissions           |
| Access Matrix         | User-permission model         |
| Capability Management | User holds permission tickets |

---

## 1️⃣5️⃣ UNIX File System

### Core Structure

Hierarchical tree of directories and files.

### Main Components

| Component     | Description                       |
| ------------- | --------------------------------- |
| Directories   | Store file names and pointers to their correponding indoes.        |
| Regular Files | Data streams                      |
| Volume Layout | Boot block, superblock            |
| Inode         | Stores metadata & block addresses |

### Inode Contains

Permissions – Timestamps – Size – Owner – **Pointers to data blocks**

---

## 1️⃣6️⃣ Linux Virtual File System (VFS) Architecture

- VFS provides a **common interface** that acts as a **universal translator** for all file systems.

- It provides a single, uniform API for all user application.

```
Applications
   ↓
VFS
   ↓
Actual File System (ext4, FAT, NTFS…)
   ↓
Disk
```

### VFS Data Structures

| Structure  | Role                 |
| ---------- | -------------------- |
| Superblock | File system info     |
| Inode      | File metadata        |
| Dentry     | Name → inode mapping |
| File       | Open file instance   |

---

## 1️⃣7️⃣ NTFS (Windows File System)

**NTFS** = New Technology File System
Default Windows file system.

### NTFS Volume Structure

How the disk space is physically and logically organized.

| Component    | Role              |
| ------------ | ----------------- |
| Boot Sector  | It stores key information such as the cluster size, the location of the MFT, and boot code used to start Windows. If this sector is damaged, the volume may become unbootable.       |
| MFT          | It's a database containing a record for every file and directory on the volume, including system files. Each record holds file attributes, names, and data locations.  |
| MFT Mirror   | Backup of MFT     |
| Log File     | Journaling        |
| Cluster Heap | The main data storage area where the actual contents of 
files are stored in clusters |

### NTFS File Storage
How each file and its metadata are stored inside the NTFS system

- **Component**:
    1. **File Record Layout**: Each record includes: File Record Header – identification number, status, and size.

    2. **File Attributes**: All information about a file is stored as a set of attributes.
- **How NTFS stores file data**
| Type         | Description             |
| ------------ | ----------------------- |
| Resident     | Small file < 700 bytes, inside MFT  |
| Non-Resident | Large file in data area(Cluster Heap) |

### NTFS Key Features

- **Centralized Metadata (MFT)**: each file or folder has a file contains name, size, permisssions, data place.

- **Security**: Support Access Control Lists, Encrypting File System

- **Fault Tolerance (Reliability)**: use log files.

- **Support for Large Files and Volumes**

- **File Compression**

- **Disk Quotas**
