# Permissions

Permissions are used to control who can access files and folders and what actions they can perform. In Windows Server, there are two main types of permissions:

- Security (NTFS) Permissions
- Share Permissions

---

# Security (NTFS) Permissions

Security permissions, also called **NTFS permissions**, are used to control access to files and folders stored on an **NTFS** partition.

> **Note:** NTFS permissions can only be applied to drives or partitions formatted with the **NTFS** file system.

By default, NTFS permissions are **inherited** from the parent folder. This means that files and folders automatically receive the permissions of their parent unless inheritance is disabled.

---

# Types of NTFS Permissions

### Full Control

Allows the user to read, write, modify, delete files and folders, and change permissions.

### Modify

Allows the user to read, write, modify, and delete files, but not change permissions.

### Read & Execute

Allows the user to open and run files or applications.

### List Folder Contents

Allows the user to view the files and folders inside a directory.

### Read

Allows the user to open and read files.

### Write

Allows the user to create new files and modify existing files.

---

# Lab Requirement

To perform this lab, I used two virtual machines:

- **System 1:** Domain Controller (Windows Server)
- **System 2:** Windows Client / Member Server

I created domain users in Active Directory and used them to test different permission levels on shared folders.

---

# Applying NTFS Permissions

I created a folder on the Domain Controller and assigned different permissions to different users.

### Steps

1. Create a folder on an **NTFS** drive.
2. Right-click the folder and select **Properties**.
3. Open the **Security** tab.
4. Click **Edit**.
5. Select **Add**.
6. Enter the domain user or group name.
7. Click **Check Names**.
8. Click **OK**.
9. Select the required permission.
10. Click **Apply** and **OK**.

I then logged in from the client computer using different domain user accounts to verify whether each user could access the folder according to the permissions assigned.

---

# Share Permissions

Share permissions control access to folders that are shared over the network.

Unlike NTFS permissions, **Share Permissions** can be applied to both **NTFS** and **FAT/FAT32** partitions.

> **Note:** Share permissions are applied only to **shared folders**, not to individual files.

---

# What is a Shared Folder?

A shared folder is a folder that is made available over the network so that other users or computers can access it.

For example, a company may create a shared folder to store documents, reports, or project files that multiple employees need to access.

---

# Types of Share Permissions

### Read

Allows users to view files and folders but prevents them from making changes.

### Change

Allows users to read, create, edit, and delete files and folders.

### Full Control

Allows users complete access, including changing share permissions.

---

# Applying Share Permissions

### Steps

1. Create a folder.
2. Right-click the folder and select **Properties**.
3. Open the **Sharing** tab.
4. Click **Advanced Sharing**.
5. Select **Share this folder**.
6. Click **Permissions**.
7. Remove the **Everyone** group if required.
8. Add the required domain user or group.
9. Assign **Read**, **Change**, or **Full Control** permission.
10. Click **Apply** and **OK**.

After sharing the folder, I accessed it from the client computer using the assigned domain user account to verify that the configured permissions were working correctly.

---

# NTFS Permissions vs Share Permissions

| NTFS Permissions | Share Permissions |
|------------------|-------------------|
| Applied to files and folders | Applied only to shared folders |
| Works only on NTFS partitions | Works on NTFS and FAT/FAT32 partitions |
| Can be applied to local and network access | Applies only when accessing over the network |
| More detailed security options | Provides basic network access control |

> **Note:** When both NTFS and Share Permissions are applied, Windows enforces the **most restrictive permission** for network access.

---

# Share Folder Management

## Applying Share Permissions

After creating the folder, I shared it over the network so that domain users could access it from their client computers.

### Steps

1. Right-click the folder and select **Properties**.
2. Open the **Sharing** tab.
3. Click **Advanced Sharing**.
4. Select **Share this folder**.
5. Click **Permissions**.
6. Remove the **Everyone** group if required.
7. Click **Add** and select the required domain user or group.
8. Assign the required permission (**Read**, **Change**, or **Full Control**).
9. Click **Apply** and then **OK**.

After sharing the folder, I tested access from the client machine using different domain user accounts.

---

# Creating a Hidden Shared Folder

A hidden shared folder is not visible when users browse the network. However, users who know the exact folder path can still access it if they have permission.

To create a hidden share, add a **$** symbol at the end of the share name.

### Example

Folder Name:

```text
Projects
```

Share Name:

```text
Projects$
```

Users can access it only by entering the full network path.

Example:

```text
\\DC01\Projects$
```

---

# Mapping a Network Drive

A mapped network drive allows users to access a shared folder as if it were a local drive.

For example, a shared folder can be mapped to the **Z:** drive.

### Steps

1. Open **File Explorer**.
2. Right-click **This PC**.
3. Select **Map Network Drive**.
4. Choose a drive letter (Example: **Z:**).
5. Enter the shared folder path.
6. Select **Reconnect at sign-in** if required.
7. Click **Finish**.

Example UNC Path:

```text
\\DC01\Projects
```

After mapping, the shared folder appears as the **Z:** drive in File Explorer.

---

# Access-Based Enumeration (ABE)

Access-Based Enumeration (ABE) is a feature that hides files and folders that a user does not have permission to access.

For example, if two users access the same shared folder, each user will only see the folders they have permission to open. Restricted folders remain hidden, improving security and reducing confusion.

---

# UNC Path (Universal Naming Convention)

A **UNC Path** is the standard format used to access shared folders over a network.

**Format:**

```text
\\ServerName\ShareName
```

**Examples:**

```text
\\DC01\Projects
```

```text
\\DC01\HR$
```

UNC paths allow users to access shared folders without knowing the physical location of the files.

---

# What I Learned

In this lab, I learned how to create shared folders, assign Share Permissions, create hidden shares using the **$** symbol, map shared folders as network drives, use UNC paths to access resources, and enable Access-Based Enumeration to improve security by showing users only the folders they are authorized to access.
