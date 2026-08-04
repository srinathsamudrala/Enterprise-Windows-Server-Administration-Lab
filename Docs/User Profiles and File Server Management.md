
# User Profile Management and File Server Resource Management (FSRM)

## What is a User Profile?

A user profile stores a user's personal settings, desktop, documents, applications, and other preferences. Whenever a user signs in, Windows loads the user's profile so they can access their personalized environment.

---

# Types of User Profiles

## Local Profile

A Local Profile is stored on the computer where the user logs in. It is available only on that computer.

**Example:**

If User1 logs in to Client-01, the profile is created only on Client-01.

---

## Roaming Profile

A Roaming Profile is stored on a shared folder on the server. Whenever the user logs in to any domain-joined computer, the same profile is downloaded from the server.

This allows users to have the same desktop, documents, and settings on different computers.

---

# Lab 1 - Creating a Local Profile

## Lab Requirement

- System 1 - Domain Controller (Windows Server)
- System 2 - Windows Client / Member Server

---

## Creating Domain Users

1. Open **Active Directory Users and Computers (ADUC)**.
2. Create the following users:
   - User1
   - User2
   - User3

---

## Verification

1. Go to the client computer.
2. Join it to the domain.
3. Sign in as **User1**.
4. Windows automatically creates a local profile for User1.
5. Repeat the same for User2 and User3 if required.

The profile is stored locally on the client computer.

Default Location:

```text
C:\Users\User1
```

---

# Creating a Roaming Profile

A Roaming Profile allows users to use the same profile from any domain computer.

---

## Steps

1. Create a shared folder on the Domain Controller.

Example:

```text
D:\Profiles
```

2. Share the folder.

Example Share Name:

```text
Profiles$
```

3. Give the required Share and NTFS permissions.

4. Open **Active Directory Users and Computers**.

5. Open the properties of **User1**.

6. Open the **Profile** tab.

7. Under **Profile Path**, enter:

```text
\\DC01\Profiles$\User1
```

8. Repeat the same for User2.

9. Click **Apply** and **OK**.

---

## Verification

1. Log in to the client computer as **User1**.
2. Windows creates the roaming profile on the server.
3. Sign out.
4. Log in to another domain computer using User1.
5. The same desktop, files, and settings will be available.

---

# How to Check Whether a Profile is Local or Roaming

### Method 1

Open:

```text
System Properties → Advanced → User Profiles → Settings
```

Windows displays all profiles available on the computer.

---

### Method 2

Open the user's properties in **Active Directory Users and Computers**.

If the **Profile Path** field is empty, the user is using a Local Profile.

If the **Profile Path** contains a network path (UNC Path), the user is using a Roaming Profile.

Example:

```text
\\DC01\Profiles$\User1
```

---

# Home Folder

## What is a Home Folder?

A Home Folder is a personal network folder assigned to a user. It provides a dedicated location where users can store their files on the server instead of saving them on the local computer.

This makes backup and file management easier.

---

# Lab - Creating a Home Folder

## Steps

1. Create a folder on the server.

Example:

```text
D:\HomeFolder
```

2. Share the folder.

3. Assign the required Share and NTFS permissions.

4. Open **Active Directory Users and Computers**.

5. Open the user's **Properties**.

6. Select the **Profile** tab.

7. Under **Home Folder**, select:

```text
Connect
```

8. Select a drive letter.

Example:

```text
H:
```

9. Enter the network path.

Example:

```text
\\DC01\HomeFolder\User1
```

10. Click **Apply** and **OK**.

---

## Verification

Log in as User1.

Open **This PC**.

The Home Folder appears as a mapped network drive.

Example:

```text
H: Home Folder
```

---

# File Server Resource Manager (FSRM)

## What is FSRM?

File Server Resource Manager (FSRM) is a Windows Server feature used to manage storage on file servers. It helps administrators control disk usage, block unwanted file types, and generate storage reports.

---

# Features of FSRM

## Storage Quota Management

Storage Quotas are used to limit the amount of disk space users or folders can consume.

Example:

A user can be limited to **5 GB** of storage.

---

## File Screening Management

File Screening prevents users from saving unwanted file types.

Examples:

- .mp3
- .mp4
- .exe
- .iso

This helps maintain security and save storage space.

---

## Storage Reports Management

Storage Reports provide detailed information about files stored on the server.

Reports can show:

- Large files
- Duplicate files
- File owners
- File types
- Storage usage

These reports help administrators monitor and manage server storage efficiently.

---

# What I Learned

In this lab, I learned the difference between Local Profiles and Roaming Profiles, created user profiles, configured roaming profiles using a shared folder, assigned Home Folders with mapped network drives, and explored File Server Resource Manager (FSRM) to manage storage, apply quotas, block unwanted file types, and generate storage reports.
````
