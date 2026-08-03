# Active Directory (AD)
# What is Active Directory?

Active Directory (AD) is a service in Windows Server that helps manage users, computers, groups, and other network resources from one central place. Instead of configuring every computer one by one, an administrator can manage everything from a single server.

# Why is Active Directory Used?

The main purpose of Active Directory is to make administration simple and secure.

Using Active Directory, we can:

Create and manage user accounts.
Add computers to the domain.
Create groups and assign permissions.
Organize users and computers using Organizational Units (OUs).
Apply Group Policies to users and computers.
Control who can access files, folders, printers, and other resources.


# Requirements Before Deploying a Domain Controller

After setting up Windows Server, there are a few basic configurations that should be completed before promoting the server to a Domain Controller.

The first step is to rename the server. Giving the server a meaningful name makes it easier to identify when multiple servers are added to the environment.

Next, I configured a static IP address. A Domain Controller should always use a static IP because services like Active Directory and DNS depend on a fixed IP address. If the IP changes, clients may not be able to locate the server.

I then verified the computer name, date and time, and time zone. These settings are important because incorrect time can cause authentication and domain-related issues.

I also checked the network connection to make sure the server could communicate properly on the network.


# Installing Active Directory Domain Services (AD DS)

After completing the basic server configuration, I installed the **Active Directory Domain Services (AD DS)** role using **Server Manager**. This role is required before a Windows Server can be promoted to a Domain Controller.

## Steps to Install AD DS

1. Open **Server Manager**.
2. Click **Manage** in the top-right corner.
3. Select **Add Roles and Features**.
4. Click **Next** on the "Before You Begin" page.
5. Select **Role-based or feature-based installation** and click **Next**.
6. Select the local server from the server pool and click **Next**.
7. Under **Server Roles**, select **Active Directory Domain Services (AD DS)**.
8. When prompted, click **Add Features** to install the required management tools.
9. Click **Next** through the remaining pages.
10. Review the selected roles and click **Install**.
11. Wait for the installation to complete and click **Close**.

> **Note:** At this stage, the server only has the AD DS role installed. It is **not yet a Domain Controller**.

---

# Promoting the Server to a Domain Controller

After installing the AD DS role, the next step was to promote the server to a Domain Controller. During this process, I created a new Active Directory forest and domain.

## Steps to Promote the Server

1. Open **Server Manager**.
2. Click the **Notification** flag at the top-right corner.
3. Select **Promote this server to a domain controller**.
4. Choose **Add a new forest**.
5. Enter the **Root Domain Name** (Example: `company.local`).
6. Click **Next**.
7. Select the **Forest Functional Level** and **Domain Functional Level**.
8. Enter the **Directory Services Restore Mode (DSRM)** password.
9. Click **Next** and continue with the default settings.
10. Ignore the DNS delegation warning if this is the first Domain Controller in the lab.
11. Review the configuration and click **Install**.
12. The server will perform a prerequisite check.
13. If no critical issues are found, the installation will continue.
14. After the installation is complete, the server will restart automatically.

---

# Verification

After the restart, I signed in using the domain administrator account and verified that the Domain Controller was working correctly.

I confirmed the installation by opening:

- Active Directory Users and Computers (ADUC)
- Active Directory Administrative Center (ADAC)
- DNS Manager
- Group Policy Management
- Server Manager

I also confirmed that the server had been successfully promoted to a Domain Controller and that the Active Directory services were running properly.

# How to check Server or Client: 
Run net accounts in Command Prompt to identify whether the machine is a Windows Server (Domain Controller) or a Windows Workstation.

# Why is DNS important? 
DNS translates server names into IP addresses, allowing clients to locate and communicate with the Domain Controller.

# What is a Server? 
A server is a computer that provides services such as Active Directory, DNS, DHCP, and authentication to client computers.

# What is a Client (Workstation)? 
A client is a computer that connects to the server to access domain resources and services.

# NTDS.DIT: 
The NTDS.DIT file is the Active Directory database that stores information about users, groups, computers, and other domain objects.
By default, it is stored in the following location:

C:\Windows\NTDS\NTDS.dit

# Domain Controller (DC): 
A Domain Controller is a Windows Server that manages Active Directory and authenticates users and computers in the domain.

# Domain: 
A domain is a logical group of users, computers, and resources managed together by Active Directory.


## SYSVOL

The **SYSVOL** folder stores Group Policy Objects (GPOs), logon scripts, and other files that are shared and replicated between all Domain Controllers.

**Default Location:**

```text
C:\Windows\SYSVOL
```

---

## Active Directory Logs

Active Directory logs can be viewed using **Event Viewer**.

**Steps:**

1. Open **Event Viewer**.
2. Navigate to:

```text
Windows Logs
 ├── Application
 ├── Security
 ├── System
```

For Active Directory-specific logs:

```text
Applications and Services Logs
 └── Directory Service
```

These logs help troubleshoot authentication, replication, DNS, and other Active Directory issues.

---

# Installing Windows Client Operating System

After configuring the Domain Controller, I created a new virtual machine for the client system. I mounted the **Windows 10** or **Windows 11 ISO** and completed the Windows installation.

During the setup, I selected the required language, keyboard layout, and edition of Windows. After the installation finished, I created a local administrator account and completed the initial Windows setup.

Before joining the client to the domain, I configured the client's network settings and set the **Preferred DNS Server** to the IP address of the Domain Controller so that the client could locate the domain.

---

# Joining the Client to the Domain

After installing the Windows client, I joined it to the Active Directory domain.

### Steps

1. Open **This PC** and select **Properties**.
2. Click **Rename this PC (Advanced)** or **Change settings**.
3. Under the **Computer Name** tab, click **Change**.
4. Select **Domain**.
5. Enter the domain name (Example: `company.local`).
6. Click **OK**.
7. Enter the **Domain Administrator** username and password when prompted.
8. Click **OK** to authorize the domain join.
9. Restart the client computer.

After the restart, the client becomes a member of the domain, and users can sign in using their domain accounts.
