# Active Directory Roles

## What are Active Directory Roles?

Active Directory uses different roles to manage and control domain operations. These roles ensure that Active Directory functions correctly, allows multiple Domain Controllers to work together, and prevents conflicts when managing domain objects.

There are two types of Active Directory operation roles:

- Multi-Master Operation Roles (MMOR)
- Flexible Single Master Operation (FSMO) Roles

---

# Multi-Master Operation Role (MMOR)

In Active Directory, every Domain Controller can perform most administrative tasks, such as creating users, groups, computers, and Organizational Units (OUs). This is known as the **Multi-Master Model**.

When a change is made on one Domain Controller, it is automatically replicated to the other Domain Controllers.

### Example

If a user account is created on **DC01**, the same user account is automatically replicated to **DC02** through Active Directory replication.

### Common Multi-Master Operations

- Create users
- Delete users
- Create groups
- Create Organizational Units (OUs)
- Reset passwords
- Create computer accounts
- Modify user properties
- Apply Group Policies

These operations can be performed on any Domain Controller.

---

# Flexible Single Master Operation (FSMO)

Some Active Directory tasks cannot be performed by multiple Domain Controllers at the same time. To avoid conflicts, Microsoft assigns these tasks to a single Domain Controller. These special tasks are called **Flexible Single Master Operations (FSMO)**.

There are **five FSMO roles** in Active Directory.

---

## Schema Master

**Purpose:** Manages changes to the Active Directory schema.

**Use:**

- Add new object types
- Modify schema attributes
- Extend the Active Directory schema

**Example:**

Installing Microsoft Exchange Server updates the Active Directory schema.

---

## Domain Naming Master

**Purpose:** Controls the creation and removal of domains in the forest.

**Use:**

- Create a new domain
- Add a child domain
- Add a tree domain
- Remove a domain

---

## RID Master

**Purpose:** Assigns unique Relative Identifier (RID) pools to Domain Controllers.

**Use:**

Every new user, group, or computer receives a unique Security Identifier (SID), ensuring there are no duplicate IDs in the domain.

---

## PDC Emulator

**Purpose:** Handles important domain operations and acts as the primary Domain Controller for specific tasks.

**Use:**

- Password changes
- Password authentication
- Time synchronization
- Account lockout processing
- Group Policy updates

---

## Infrastructure Master

**Purpose:** Updates object references between different domains.

**Use:**

- Maintains group memberships across domains
- Updates references when objects are moved or renamed

---

# Forest-Level FSMO Roles

These roles exist only once in an Active Directory forest.

- Schema Master
- Domain Naming Master

---

# Domain-Level FSMO Roles

These roles exist once in each Active Directory domain.

- RID Master
- PDC Emulator
- Infrastructure Master

---

# MMOR vs FSMO

| Multi-Master Operation Role (MMOR) | Flexible Single Master Operation (FSMO) |
|------------------------------------|------------------------------------------|
| All Domain Controllers can perform the operation. | Only one Domain Controller performs the operation. |
| Changes are replicated to other Domain Controllers. | Special operations are handled by a single role owner. |
| Used for day-to-day administration. | Used for critical Active Directory operations. |
| Supports multiple write operations. | Prevents conflicts during unique operations. |

---

# Summary

- **MMOR (Multi-Master Operation Role):** Allows all Domain Controllers to create and manage most Active Directory objects, with changes replicated automatically.

- **FSMO (Flexible Single Master Operation):** Handles special operations that must be performed by only one Domain Controller to maintain consistency and prevent conflicts.
```
