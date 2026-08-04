# Backup Domain Controller (Additional Domain Controller) and Active Directory Replication

## What is an Additional Domain Controller (ADC)?

An Additional Domain Controller (ADC) is another Windows Server that is promoted to a Domain Controller in an existing Active Directory domain. It maintains a copy of the Active Directory database and continuously synchronizes with the primary Domain Controller.

Having more than one Domain Controller improves availability, fault tolerance, and ensures users can still authenticate even if one Domain Controller becomes unavailable.

---

# Why Do We Need an Additional Domain Controller?

An Additional Domain Controller provides:

- High Availability
- Fault Tolerance
- Load Balancing
- Active Directory Replication
- Backup Authentication Services
- Improved Performance for Multiple Sites

If the primary Domain Controller fails, users can continue logging in using the Additional Domain Controller.

---

# Active Directory Architecture

```text
                    company.local

                 ┌───────────────┐
                 │     DC01      │
                 │ Primary DC    │
                 │ DNS + AD DS   │
                 └───────┬───────┘
                         │
              Active Directory
                 Replication
                         │
                 ┌───────▼───────┐
                 │     DC02      │
                 │ Additional DC │
                 │ DNS + AD DS   │
                 └───────────────┘
```

Both Domain Controllers contain the same Active Directory database and replicate changes automatically.

---

# Lab Requirement

For this lab, I used the following virtual machines.

| System | Role |
|---------|------|
| System 1 | Primary Domain Controller (DC01) |
| System 2 | Additional Domain Controller (DC02) |

Both servers were connected to the same virtual network.

---

# Prerequisites

Before promoting the second server, I completed the following configuration.

- Installed Windows Server.
- Configured a Static IP Address.
- Configured the Preferred DNS Server to point to the Primary Domain Controller.
- Verified network connectivity using Ping.
- Joined the server to the existing Active Directory domain.
- Logged in using Domain Administrator credentials.

---

# Step 1 - Join the Server to the Existing Domain

Before promoting the server, it must first become a member server.

### Steps

1. Open **This PC**.
2. Select **Properties**.
3. Click **Change Settings**.
4. Click **Change**.
5. Select **Domain**.
6. Enter the existing domain name.

Example

```text
company.local
```

7. Enter the Domain Administrator username and password.
8. Restart the server.

After restarting, the server becomes a member of the existing domain.

---

# Step 2 - Install Active Directory Domain Services

1. Open **Server Manager**.
2. Click **Manage**.
3. Select **Add Roles and Features**.
4. Select **Role-based or Feature-based Installation**.
5. Select the local server.
6. Select **Active Directory Domain Services**.
7. Click **Add Features**.
8. Click **Next**.
9. Click **Install**.

Wait until the installation completes.

---

# Step 3 - Promote to an Additional Domain Controller

1. Open **Server Manager**.
2. Click the Notification Flag.
3. Select **Promote this server to a domain controller**.
4. Choose:

```
Add a domain controller to an existing domain
```

5. Enter the existing domain.

Example

```
company.local
```

6. Enter Domain Administrator credentials.
7. Select

- DNS Server
- Global Catalog

8. Select the Active Directory Site.

(Default-First-Site-Name)

9. Enter the DSRM Password.

10. Continue with the default configuration.

11. Complete the Prerequisite Check.

12. Click **Install**.

The server restarts automatically.

---

# Verification

After the restart, verify that the promotion was successful.

Open

- Active Directory Users and Computers
- Active Directory Sites and Services
- DNS Manager
- Event Viewer

Verify that both Domain Controllers are listed.

---

# What is Active Directory Replication?

Active Directory Replication is the process of copying Active Directory changes from one Domain Controller to another.

Whenever a user, group, password, or computer is created or modified, the changes are automatically synchronized to all Domain Controllers.

This ensures that every Domain Controller has the same Active Directory information.

---

# How Replication Works

Example

```
Create User
      │
      ▼
   DC01
      │
Replication
      │
      ▼
   DC02
```

If a new user is created on DC01, the same user automatically appears on DC02 after replication.

---

# Types of Replication

## Intra-Site Replication

Occurs between Domain Controllers located in the same Active Directory Site.

It is fast because high-speed network connectivity is assumed.

---

## Inter-Site Replication

Occurs between Domain Controllers located in different Active Directory Sites.

Replication is optimized to reduce bandwidth usage.

---

# How to Verify Replication

### Method 1

Open

```
Active Directory Sites and Services
```

Expand

```
Sites

Default-First-Site-Name

Servers
```

Both Domain Controllers should appear.

---

### Method 2

Open Command Prompt

Run

```cmd
repadmin /replsummary
```

Displays the replication health.

---

Run

```cmd
repadmin /showrepl
```

Shows replication partners.

---

Run

```cmd
dcdiag
```

Checks Domain Controller health.

---

Run

```cmd
dcdiag /test:dns
```

Checks DNS configuration.

---

# Common Replication Problems

Some common issues include:

- DNS misconfiguration
- Network connectivity issues
- Firewall blocking replication ports
- Incorrect system time
- Authentication failures
- Active Directory database corruption
- SYSVOL replication issues

---

# Troubleshooting Replication

### Check Network Connectivity

```cmd
ping DC01
```

---

### Verify DNS

```cmd
nslookup company.local
```

---

### Check Replication Status

```cmd
repadmin /replsummary
```

---

### Display Replication Details

```cmd
repadmin /showrepl
```

---

### Force Replication

```cmd
repadmin /syncall /AdeP
```

---

### Check Domain Controller Health

```cmd
dcdiag
```

---

### Verify Event Logs

Open

```
Event Viewer

Applications and Services Logs

Directory Service
```

Review any replication or Active Directory errors.

---

# Best Practices

- Deploy at least two Domain Controllers.
- Configure static IP addresses.
- Use Active Directory-integrated DNS.
- Monitor replication regularly.
- Keep system time synchronized.
- Perform regular system state backups.
- Monitor Event Viewer for replication errors.

---

# What I Learned

In this lab, I deployed an Additional Domain Controller in an existing Active Directory domain and configured Active Directory replication between both Domain Controllers. I verified replication using built-in Windows tools and command-line utilities, and I learned how replication ensures high availability, fault tolerance, and consistent Active Directory data across the environment. I also explored common replication issues and the troubleshooting steps used by Windows administrators to maintain a healthy Active Directory infrastructure.
