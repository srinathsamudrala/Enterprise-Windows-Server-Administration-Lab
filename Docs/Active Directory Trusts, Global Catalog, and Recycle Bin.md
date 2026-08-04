# Active Directory Trusts, Global Catalog, and Active Directory Recycle Bin

## What is a Trust Relationship?

A **Trust Relationship** is a secure connection between two domains or forests that allows users in one domain to access resources in another domain. Trusts simplify resource sharing while maintaining security.

---

# Why are Trust Relationships Used?

Trust relationships allow organizations to:

- Share resources between domains.
- Authenticate users across domains.
- Reduce the need to create duplicate user accounts.
- Support collaboration between different departments or organizations.

---

# Trust Relationship Categories

Active Directory supports two main trust categories.

## Transitive Trust

A **Transitive Trust** automatically extends trust to all connected domains.

### Example

```text
company.local
      │
      │
hr.company.local
      │
      │
sales.company.local
```

If **company.local** trusts **hr.company.local**, and **hr.company.local** trusts **sales.company.local**, then **company.local** automatically trusts **sales.company.local**.

---

## Non-Transitive Trust

A **Non-Transitive Trust** exists only between two specified domains.

No additional trust relationships are created automatically.

### Example

```text
company.local  ─────────► partner.local
```

Only these two domains trust each other.

---

# Trust Direction

Trust direction defines the flow of authentication between domains.

---

## One-Way Incoming Trust

Users from another domain can access resources in the current domain.

```text
Domain A  ◄──────── Domain B
```

Domain A accepts authentication requests from Domain B.

---

## One-Way Outgoing Trust

Users in the current domain can access resources in another domain.

```text
Domain A ─────────► Domain B
```

Domain A trusts Domain B.

---

## Two-Way Trust

Both domains trust each other.

Users from either domain can access resources in the other domain if they have permission.

```text
Domain A ◄────────► Domain B
```

---

# Types of Trusts

Active Directory supports several trust types.

---

## 1. Parent-Child Trust

Created automatically when a child domain is added.

Example

```text
company.local
      │
hr.company.local
```

- Automatic
- Two-Way
- Transitive

---

## 2. Tree-Root Trust

Created automatically between the root domains of different trees within the same forest.

Example

```text
Forest

company.local

school.local
```

- Automatic
- Two-Way
- Transitive

---

## 3. External Trust

Used to connect two separate domains that are not in the same forest.

```text
company.local ◄────► partner.local
```

- Manual
- Non-Transitive

---

## 4. Forest Trust

Connects two different Active Directory forests.

```text
Forest A

company.local

◄────────────►

Forest B

school.local
```

- Manual
- Transitive

---

## 5. Shortcut Trust

Creates a shorter authentication path between two domains in the same forest.

```text
company.local
      │
      │
finance.company.local

        ▲
        │
Shortcut Trust
        │
sales.company.local
```

This improves authentication performance.

---

# Global Catalog (GC)

## What is a Global Catalog?

A **Global Catalog (GC)** is a special role assigned to a Domain Controller that stores a partial copy of every object in the Active Directory forest.

Instead of searching every domain, users can search the Global Catalog to quickly locate objects.

---

# Main Uses of Global Catalog

- Faster Active Directory searches.
- User logon authentication.
- Universal Group Membership lookup.
- Searching users, groups, and computers across the forest.
- Improves authentication performance.

---

# Example

```text
Forest

        GC

         │

 ┌───────┼────────┐

company.local

hr.company.local

sales.company.local
```

The Global Catalog can search all domains without contacting every Domain Controller individually.

---

# Active Directory Recycle Bin

## What is the Active Directory Recycle Bin?

The **Active Directory Recycle Bin** is a feature that allows administrators to recover accidentally deleted Active Directory objects without restoring a system backup.

It helps restore:

- Users
- Groups
- Organizational Units (OUs)
- Computer Accounts

along with their attributes.

---

# Benefits

- Quick object recovery.
- No need for authoritative restore.
- Restores group memberships.
- Restores object permissions.
- Reduces downtime.

---

# Phases of the Active Directory Recycle Bin

## Phase 1 - Active Object

The object exists normally in Active Directory.

Example:

```text
User1
```

The object is available for use.

---

## Phase 2 - Deleted Object

When an object is deleted, it enters the Deleted Objects container.

It can still be restored with all its attributes.

---

## Phase 3 - Recycled Object

After the deleted object lifetime expires, it becomes a Recycled Object.

Most of its attributes are removed, making full recovery no longer possible.

---

## Phase 4 - Permanently Deleted

After the recycle lifetime expires, the object is permanently removed from Active Directory.

It cannot be recovered unless a backup is available.

---

# Enabling the Active Directory Recycle Bin

### Steps

1. Open **Active Directory Administrative Center (ADAC)**.
2. Select the domain or forest.
3. In the **Tasks** pane, click **Enable Recycle Bin**.
4. Confirm the action.
5. Allow Active Directory replication to complete.

> **Note:** Once enabled, the Active Directory Recycle Bin cannot be disabled.

---

# Restoring a Deleted Object

### Steps

1. Open **Active Directory Administrative Center (ADAC)**.
2. Open the **Deleted Objects** container.
3. Select the required object.
4. Click **Restore** or **Restore To**.
5. Verify that the object has been successfully restored.

---

# What I Learned

In this section, I learned how trust relationships allow communication between different domains and forests, the differences between transitive and non-transitive trusts, one-way and two-way trust directions, and the five trust types used in Active Directory. I also explored the purpose of the Global Catalog for fast object searches and user authentication, and learned how the Active Directory Recycle Bin helps recover deleted objects without restoring from backup.
````
