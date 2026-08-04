# FSMO Roles (Flexible Single Master Operations)

## What are FSMO Roles?

Although Active Directory uses multi-master replication, some operations can only be performed by one Domain Controller at a time. These special operations are handled by **FSMO (Flexible Single Master Operations) Roles**.

There are **five FSMO roles** in an Active Directory forest.

- Schema Master
- Domain Naming Master
- RID Master
- PDC Emulator
- Infrastructure Master

---

# Types of FSMO Roles

## 1. Schema Master

The **Schema Master** manages changes to the Active Directory schema.

The schema defines the structure of Active Directory objects such as users, groups, and computers.

### Example

When Microsoft Exchange Server is installed, new attributes are added to the Active Directory schema. Only the **Schema Master** can perform these changes.

---

## 2. Domain Naming Master

The **Domain Naming Master** controls the creation and deletion of domains within a forest.

### Example

- Add a Child Domain
- Add a Tree Domain
- Remove a Domain

Only the Domain Naming Master can perform these tasks.

---

## 3. RID Master

The **RID (Relative Identifier) Master** allocates unique RID pools to Domain Controllers.

Every user, group, and computer created in Active Directory receives a unique **Security Identifier (SID)**.

The RID Master ensures there are no duplicate SIDs.

### Example

Creating:

- User1
- User2
- Computer01

Each object receives a unique SID.

---

## 4. PDC Emulator

The **Primary Domain Controller (PDC) Emulator** is one of the most important FSMO roles.

It performs tasks such as:

- Password changes
- Password authentication
- Time synchronization
- Group Policy updates
- Account lockout processing

### Example

When a user changes their password, the PDC Emulator immediately updates the password and shares it with other Domain Controllers.

---

## 5. Infrastructure Master

The **Infrastructure Master** updates object references between different domains.

It ensures that group memberships remain accurate when users belong to different domains.

---

# Forest-Level Roles

These roles exist once per forest.

- Schema Master
- Domain Naming Master

---

# Domain-Level Roles

These roles exist in every domain.

- RID Master
- PDC Emulator
- Infrastructure Master

---

# Lab Requirement

For this lab, I used:

- DC01 (Primary Domain Controller)
- DC02 (Additional Domain Controller)

Both servers were configured in the same Active Directory domain.

---

# Checking FSMO Roles

Open **Command Prompt** with Administrator privileges.

Run:

```cmd
netdom query fsmo
```

The output displays which Domain Controller currently owns each FSMO role.

---

# Viewing FSMO Roles Using GUI

### Active Directory Users and Computers

View:

- RID Master
- PDC Emulator
- Infrastructure Master

Steps:

1. Open **ADUC** (`dsa.msc`).
2. Right-click the domain.
3. Select **Operations Masters**.

---

### Active Directory Domains and Trusts

View:

- Domain Naming Master

Steps:

1. Open **Active Directory Domains and Trusts**.
2. Right-click **Active Directory Domains and Trusts**.
3. Select **Operations Master**.

---

### Active Directory Schema

View:

- Schema Master

Steps:

1. Register the schema snap-in.

```cmd
regsvr32 schmmgmt.dll
```

2. Open **MMC**.

```cmd
mmc
```

3. Add the **Active Directory Schema** snap-in.
4. Right-click **Active Directory Schema**.
5. Select **Operations Master**.

---

# Transferring FSMO Roles

## What is Role Transfer?

A **Role Transfer** is the planned movement of FSMO roles from one healthy Domain Controller to another.

This is commonly performed during:

- Hardware upgrades
- Server maintenance
- Operating system upgrades
- Server replacement

Both Domain Controllers must be online.

---

# Transfer FSMO Roles Using GUI

### RID Master, PDC Emulator, Infrastructure Master

1. Open **ADUC**.
2. Right-click the domain.
3. Select **Operations Masters**.
4. Select the required role.
5. Click **Change**.
6. Confirm the transfer.

---

### Domain Naming Master

1. Open **Active Directory Domains and Trusts**.
2. Right-click the root.
3. Select **Operations Master**.
4. Click **Change**.

---

### Schema Master

1. Open **MMC**.
2. Add **Active Directory Schema**.
3. Right-click **Active Directory Schema**.
4. Select **Operations Master**.
5. Click **Change**.

---

# Transfer FSMO Roles Using PowerShell

Run:

```powershell
Move-ADDirectoryServerOperationMasterRole
```

Example:

```powershell
Move-ADDirectoryServerOperationMasterRole -Identity DC02 -OperationMasterRole PDCEmulator
```

---

# Transfer FSMO Roles Using NTDSUTIL

Open Command Prompt.

Run:

```cmd
ntdsutil
```

Commands:

```text
roles

connections

connect to server DC02

quit

transfer rid master

transfer pdc

transfer infrastructure master

transfer naming master

transfer schema master
```

Type:

```text
quit
quit
```

---

# Seizing FSMO Roles

## What is Role Seizure?

Role Seizure is the process of forcibly assigning FSMO roles to another Domain Controller when the original Domain Controller has permanently failed.

Unlike a role transfer, the original server is unavailable.

Role Seizure should only be performed during a disaster recovery situation.

---

# When Should Role Seizure Be Used?

Examples:

- Hardware failure
- Motherboard failure
- Disk corruption
- Server destroyed
- Server cannot be recovered

---

# Steps to Seize FSMO Roles

Open Command Prompt.

Run:

```cmd
ntdsutil
```

Commands:

```text
roles

connections

connect to server DC02

quit

seize rid master

seize pdc

seize infrastructure master

seize naming master

seize schema master
```

Exit:

```text
quit
quit
```

After the seizure, the failed Domain Controller should never be brought back online unless it is rebuilt.

---

# Verifying FSMO Roles

Run:

```cmd
netdom query fsmo
```

Verify that all roles are assigned to the new Domain Controller.

---

# Troubleshooting FSMO Issues

## Check Domain Controller Health

```cmd
dcdiag
```

---

## Verify Replication

```cmd
repadmin /replsummary
```

---

## Display Replication Details

```cmd
repadmin /showrepl
```

---

## Check DNS

```cmd
nslookup company.local
```

---

## Verify Connectivity

```cmd
ping DC02
```

---

## Review Event Logs

Open:

```text
Event Viewer

Applications and Services Logs

Directory Service
```

Review any FSMO or replication-related errors.

---

# Best Practices

- Maintain at least two Domain Controllers.
- Regularly verify FSMO role holders.
- Perform role transfers during planned maintenance.
- Use role seizure only when the original server cannot be recovered.
- Back up Domain Controllers regularly.
- Monitor replication health before and after transferring roles.

---

# What I Learned

In this lab, I learned the purpose of the five FSMO roles and how they support Active Directory operations. I practiced checking FSMO role owners, transferring roles between healthy Domain Controllers, and understood when and how to seize roles during disaster recovery. I also used Windows administrative tools and command-line utilities to verify role ownership and troubleshoot common Active Directory issues.
