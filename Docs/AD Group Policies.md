# Group Policy (GPO)

## What is Group Policy?

**Group Policy (GPO)** is a Windows Server feature used to centrally manage and control user and computer settings in an Active Directory environment. It allows administrators to enforce security settings, desktop configurations, software policies, password policies, and many other configurations across the domain.

Instead of configuring each computer individually, a Group Policy can be applied once and automatically affect all targeted users or computers.

---

# Where Can Group Policies Be Applied?

Group Policies can be linked at different levels in Active Directory.

- Local Computer
- Site
- Domain
- Organizational Unit (OU)

This allows administrators to apply different settings based on organizational requirements.

---

# Tools Used

The following tools are commonly used to manage Group Policy:

- **Group Policy Management Console (GPMC)** (`gpmc.msc`)
- **Group Policy Management Editor**
- **Active Directory Users and Computers (ADUC)** (`dsa.msc`)
- **Resultant Set of Policy (RSoP)** (`rsop.msc`)
- **Command Prompt**
- **Windows PowerShell**

---

# Lab Requirement

For this lab, I used:

| System | Purpose |
|---------|---------|
| DC01 | Domain Controller |
| Client01 | Domain-Joined Windows Client |

The client computer was joined to the domain to verify the applied Group Policies.

---

# Applying an OU-Level Group Policy

An OU-level Group Policy affects only the users and computers located inside that Organizational Unit.

### Example

```text
company.local
│
├── HR
├── IT
└── Finance
```

If a policy is linked to the **HR** OU, only users and computers in the HR OU receive that policy.

### Steps

1. Open **Group Policy Management** (`gpmc.msc`).
2. Expand the forest and domain.
3. Expand **Organizational Units (OU)**.
4. Right-click the required OU.
5. Select **Create a GPO in this domain, and Link it here**.
6. Enter a GPO name.
7. Right-click the new GPO.
8. Select **Edit**.
9. Configure the required policy.
10. Close the editor.
11. On the client computer, run:

```cmd
gpupdate /force
```

12. Verify that the policy has been applied.

---

# Applying a Domain-Level Group Policy

A Domain-level Group Policy affects all users and computers within the domain unless inheritance is blocked or overridden.

### Steps

1. Open **Group Policy Management**.
2. Expand the domain.
3. Right-click the domain name.
4. Select **Create a GPO in this domain, and Link it here**.
5. Enter a GPO name.
6. Click **Edit**.
7. Configure the required settings.
8. Close the editor.
9. Run:

```cmd
gpupdate /force
```

10. Verify the policy on the client computer.

---

# Applying a Site-Level Group Policy

A Site-level Group Policy affects all users and computers located within the selected Active Directory Site.

### Steps

1. Open **Group Policy Management**.
2. Expand **Sites**.
3. Select the required site.
4. Right-click the site.
5. Select **Create a GPO in this domain, and Link it here**.
6. Enter a name for the policy.
7. Edit the required settings.
8. Run:

```cmd
gpupdate /force
```

9. Verify the applied policy.

---

# Denying a Group Policy

Sometimes a Group Policy should not apply to a specific user or group.

This can be achieved using **Security Filtering** or **Deny Apply Group Policy** permissions.

### Steps

1. Open **Group Policy Management**.
2. Select the required GPO.
3. Open the **Delegation** tab.
4. Click **Advanced**.
5. Select the required user or group.
6. Enable **Deny** for **Apply Group Policy**.
7. Click **Apply**.
8. Run:

```cmd
gpupdate /force
```

The selected user or group will no longer receive that policy.

---

# Group Policy Hierarchy

Windows processes Group Policies in the following order:

```text
Local Policy
      │
      ▼
Site Policy
      │
      ▼
Domain Policy
      │
      ▼
Organizational Unit (OU) Policy
```

If the same setting is configured at multiple levels, the policy applied last takes precedence.

---

# Group Policy Processing Order (LSDOU)

The processing order is commonly remembered as:

```text
L → S → D → OU
```

Where:

- **L** = Local Policy
- **S** = Site Policy
- **D** = Domain Policy
- **OU** = Organizational Unit Policy

OU policies have the highest precedence because they are processed last.

---

# Block Inheritance

By default, Group Policies applied at the Site and Domain levels are inherited by Organizational Units.

**Block Inheritance** prevents an OU from receiving Group Policies from its parent containers.

### Steps

1. Open **Group Policy Management**.
2. Right-click the required **OU**.
3. Select **Block Inheritance**.
4. A blue exclamation mark appears, indicating that inheritance is blocked.

> **Note:** Policies marked as **Enforced** at a higher level will still apply even if inheritance is blocked.

---

# Useful Commands

Update Group Policy:

```cmd
gpupdate /force
```

View applied policies:

```cmd
gpresult /r
```

Generate an HTML Group Policy report:

```cmd
gpresult /h report.html
```

Open Resultant Set of Policy:

```cmd
rsop.msc
```

---

# What I Learned

In this lab, I learned how to create and manage Group Policies using the Group Policy Management Console. I applied policies at the Site, Domain, and OU levels, understood the LSDOU processing order, tested policy inheritance, blocked inheritance when required, and verified the applied settings using built-in Windows tools such as **gpupdate**, **gpresult**, and **RSoP**.
````
