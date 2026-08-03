# Active Directory Users and Computers (ADUC)

## What is ADUC?

**Active Directory Users and Computers (ADUC)** is a management tool used to create and manage users, computers, groups, and Organizational Units (OUs) in an Active Directory environment. It is one of the most commonly used tools by Windows Server administrators.

**Shortcut Command:**

```cmd
dsa.msc
```

---

# Local User vs Domain User

### Local User

A **Local User** is created on a single computer and can only log in to that computer. The account information is stored locally and cannot be used on other systems.

**Example:**

```text
PC01\User1
```

---

### Domain User

A **Domain User** is created in Active Directory and can log in to any computer that is joined to the domain, depending on the permissions assigned.

**Example:**

```text
company\User1
```

The account is stored in the Active Directory database (**NTDS.dit**) on the Domain Controller.

---

# Lab Requirements

To perform this lab, I used two virtual machines:

- **Domain Controller (Windows Server)** – Hosts Active Directory.
- **Client Machine (Windows 10/11)** – Joined to the domain for testing.

---

# Creating Domain User Accounts

After opening ADUC, I created multiple domain user accounts for testing.

**Example Users:**

- User1
- User2

While creating each user, I configured:

- First Name
- Last Name
- User Logon Name (UPN)
- Username
- Password
- Password options

These users were later used for domain login and Group Policy testing.

---

# Account Lockout Policy

I configured an **Account Lockout Policy** using Group Policy to improve security.

This policy locks a user account after a specified number of failed login attempts, helping protect the domain from unauthorized access and brute-force attacks.

---

# Unlocking a Locked User Account

If a user account becomes locked, it can be unlocked from ADUC.

**Steps:**

1. Open **Active Directory Users and Computers**.
2. Locate the user account.
3. Right-click the user and select **Properties**.
4. Open the **Account** tab.
5. Select **Unlock Account**.
6. Click **Apply** and **OK**.

---

# Resetting User Passwords

ADUC allows administrators to reset passwords without knowing the user's current password.

**Steps:**

1. Right-click the user account.
2. Select **Reset Password**.
3. Enter the new password.
4. Select the required password options.
5. Click **OK**.

This is commonly used when users forget their passwords.

---

# Configuring User Account Properties

Each user account contains additional information that can be configured.

Some commonly used properties include:

- User Logon Name
- Display Name
- Email Address
- Phone Number
- Department
- Job Title
- Office Location
- Profile Path
- Home Folder
- Logon Hours
- Logon Workstations

These settings help administrators manage users more efficiently.

---

# Organizational Unit (OU)

An **Organizational Unit (OU)** is a container used to organize users, computers, and groups inside a domain.

Instead of keeping everything in one location, OUs help separate resources based on departments or locations.

**Example:**

```text
Company.local
│
├── HR
├── IT
├── Finance
├── Sales
└── Computers
```

OUs also make it easier to apply Group Policies to specific users or departments.

---

# Security Groups

A **Security Group** is used to assign permissions to users and computers.

Instead of assigning permissions individually, users are added to a security group.

**Example:**

```text
IT_Admins
HR_Team
Finance_Users
```

Security groups are mainly used to control access to shared folders, printers, and other network resources.

---

# Distribution Groups

A **Distribution Group** is used only for sending emails to multiple users.

Unlike Security Groups, Distribution Groups cannot be used to assign permissions.

**Example:**

```text
All_Employees
HR_Announcements
Sales_Team
```

These groups are commonly used with Microsoft Exchange for email distribution.

---

# What I Learned

Through this lab, I learned how to manage users, computers, Organizational Units, and groups using Active Directory Users and Computers. I also gained hands-on experience creating domain user accounts, resetting passwords, unlocking locked accounts, configuring user properties, and organizing Active Directory objects using OUs and groups.
