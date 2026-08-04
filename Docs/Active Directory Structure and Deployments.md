# Active Directory Structure

## What is Active Directory Structure?

The Active Directory structure defines how users, computers, domains, and servers are organized in an Active Directory environment. It helps administrators manage resources efficiently and allows the network to grow as the organization expands.

Active Directory is divided into two main structures:

- Logical Structure
- Physical Structure

---

# Logical Structure

The logical structure is used to organize Active Directory objects such as users, groups, computers, and domains. It focuses on how resources are arranged and managed.

The logical structure includes:

- Domain
- Tree
- Forest
- Organizational Units (OUs)

---

## Domain

A **Domain** is the basic unit of Active Directory. It is a collection of users, computers, groups, and other resources that share the same Active Directory database and security policies.

**Example:**

```text
company.local
```

All users and computers that join this domain are managed from the Domain Controller.

---

## Tree

A **Tree** is a group of related domains that share the same namespace.

A child domain inherits part of the parent domain name and automatically establishes a trust relationship with the parent domain.

### Example

```text
company.local
        │
 ┌──────┴──────┐
 │             │
hr.company.local
it.company.local
```

In this example:

- **company.local** is the Parent Domain.
- **hr.company.local** is a Child Domain.
- **it.company.local** is another Child Domain.

All domains belong to the same tree because they share the **company.local** namespace.

---

## Forest

A **Forest** is the highest level in Active Directory.

It consists of one or more domain trees. All domains in a forest share the same Active Directory schema, configuration, and Global Catalog.

### Example

```text
                    Forest
                       │
        ┌──────────────┴──────────────┐
        │                             │
   company.local                 school.local
        │                             │
   hr.company.local             students.school.local
```

A forest allows different organizations or business units to work together while maintaining separate domain structures.

---

# Organizational Unit (OU)

An **Organizational Unit (OU)** is used to organize users, computers, and groups within a domain.

Example:

```text
company.local
│
├── HR
├── IT
├── Finance
└── Sales
```

OUs make it easier to manage resources and apply Group Policies.

---

# Physical Structure

The physical structure represents the actual hardware and network components used in Active Directory.

It includes:

- Domain Controllers
- Sites
- Site Links
- Replication

---

## Domain Controller (DC)

A Domain Controller is the server that stores the Active Directory database and authenticates users.

It also manages users, computers, groups, Group Policies, DNS, and other Active Directory services.

---

## Sites

A Site represents one or more physical network locations connected by a reliable network.

Sites help Active Directory manage authentication and replication efficiently between different office locations.

### Example

```text
Company

├── Hyderabad Site
│      └── DC01
│
├── Bengaluru Site
│      └── DC02
│
└── Chennai Site
       └── DC03
```

Each site can have its own Domain Controller to improve performance and reduce network traffic.

---

# Lab Deployment Configuration

For this project, I deployed a simple Active Directory environment using virtual machines.

### Lab Setup

- **Domain Controller (DC01)** – Windows Server
- **Client-01** – Windows 10/11
- **Client-02** – Windows 10/11 (Optional)

The Domain Controller hosts:

- Active Directory Domain Services (AD DS)
- DNS Server
- DHCP Server
- Group Policy
- File Services

Both client machines are joined to the domain and communicate with the Domain Controller.

### Lab Diagram

```text
                 Host Computer
                        │
      Oracle VirtualBox / VMware Workstation
                        │
               Virtual Network
                        │
        ┌───────────────┴───────────────┐
        │                               │
   Domain Controller               Windows Client
    Windows Server                  Windows 11
        │
        ├── Active Directory
        ├── DNS
        ├── DHCP
        ├── Group Policy
        └── File Services
```

---

# Active Directory Deployment Configurations

When promoting a Windows Server to a Domain Controller, Active Directory provides different deployment options based on the organization's requirements.

The deployment is performed using the **Active Directory Domain Services Configuration Wizard** after installing the **AD DS** role.

---

# Deployment Options

During the Domain Controller promotion, the following deployment options are available:

1. Add a Domain Controller to an Existing Domain
2. Add a New Domain to an Existing Forest
3. Add a New Forest

---

# 1. Add a Domain Controller to an Existing Domain

## Purpose

This option is used to deploy an **Additional Domain Controller (ADC)** for an existing domain. It provides redundancy, fault tolerance, load balancing, and Active Directory replication.

### Example

```text
company.local

DC01 (Existing)
        │
        │ Replication
        │
DC02 (Additional Domain Controller)
```

---

## Steps

1. Install **Active Directory Domain Services (AD DS)**.
2. Open **Server Manager**.
3. Click the **Notification** flag.
4. Select **Promote this server to a domain controller**.
5. Choose **Add a domain controller to an existing domain**.
6. Enter the domain name.
7. Provide **Domain Administrator** credentials.
8. Select the existing domain.
9. Configure:
   - DNS Server
   - Global Catalog (GC)
   - Site Name
10. Enter the **DSRM** password.
11. Continue with the default settings.
12. Complete the prerequisite check.
13. Click **Install**.
14. Wait for the server to restart.

---

# Verification

Verify using:

- Active Directory Users and Computers
- Active Directory Sites and Services
- DNS Manager
- Event Viewer
- Replication Status

---

# 2. Add a New Domain to an Existing Forest

## Purpose

This option creates a **Child Domain** or a **New Tree Domain** inside an existing forest.

It is commonly used when different departments, branches, or business units require separate domains while remaining part of the same forest.

---

### Example (Child Domain)

```text
company.local
      │
      ├── hr.company.local
      ├── it.company.local
      └── sales.company.local
```

---

## Steps

1. Install **AD DS**.
2. Open **Server Manager**.
3. Click **Promote this server to a domain controller**.
4. Select **Add a new domain to an existing forest**.
5. Choose:
   - Child Domain
   - Tree Domain
6. Enter the Parent Domain.
7. Enter the New Domain Name.
8. Provide Enterprise Administrator credentials.
9. Configure the Domain Controller options.
10. Enter the DSRM password.
11. Continue through the wizard.
12. Complete the prerequisite check.
13. Click **Install**.
14. Restart the server.

---

# Verification

Confirm that the new domain appears in:

- Active Directory Domains and Trusts
- Active Directory Users and Computers
- DNS Manager

---

# 3. Add a New Forest

## Purpose

This option is used when creating a completely new Active Directory environment.

A new forest has its own schema, configuration, Global Catalog, and security boundary.

---

### Example

```text
Forest

company.local
```

---

## Steps

1. Install **Active Directory Domain Services (AD DS)**.
2. Open **Server Manager**.
3. Click the **Notification** flag.
4. Select **Promote this server to a domain controller**.
5. Choose **Add a new forest**.
6. Enter the Root Domain Name.

Example:

```text
company.local
```

7. Select:
   - Forest Functional Level
   - Domain Functional Level
8. Enable DNS if required.
9. Configure the DSRM password.
10. Continue with the default configuration.
11. Complete the prerequisite check.
12. Click **Install**.
13. Wait for the installation to complete.
14. Restart the server.

---

# Verification

After restarting:

- Log in using the Domain Administrator account.
- Open **Active Directory Users and Computers (ADUC)**.
- Open **DNS Manager**.
- Open **Group Policy Management**.
- Verify that the new forest and domain have been created successfully.

---

# Tools Used

The following Windows Server tools are used during Active Directory deployment:

- **Server Manager** – Install server roles and features.
- **Active Directory Domain Services Configuration Wizard** – Promote the server to a Domain Controller.
- **Active Directory Users and Computers (ADUC)** – Manage users, groups, and Organizational Units.
- **Active Directory Domains and Trusts** – Manage domains, trees, forests, and trust relationships.
- **Active Directory Sites and Services** – Manage Domain Controllers, sites, and replication.
- **DNS Manager** – Configure and manage DNS records.
- **Event Viewer** – Review installation logs and troubleshoot issues.
- **Windows PowerShell** – Automate Active Directory deployment and administration.
