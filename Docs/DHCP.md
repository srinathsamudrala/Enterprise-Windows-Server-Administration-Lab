# Dynamic Host Configuration Protocol (DHCP)

## What is DHCP?

**Dynamic Host Configuration Protocol (DHCP)** is a network service that automatically assigns IP addresses and other network settings to client computers. Instead of manually configuring each device, DHCP provides the required network information automatically.

DHCP reduces administrative effort, prevents IP address conflicts, and simplifies network management.

---

# Why Do We Use DHCP?

DHCP helps administrators by:

- Automatically assigning IP addresses.
- Reducing manual configuration.
- Preventing duplicate IP addresses.
- Managing IP addresses from a central server.
- Automatically assigning network settings to new devices.

---

# Information Assigned by DHCP

When a client receives an IP address, DHCP can also provide:

- IP Address
- Subnet Mask
- Default Gateway
- DNS Server
- Domain Name
- Lease Duration

---

# DHCP Components

## DHCP Server

The DHCP Server is responsible for assigning IP addresses and network settings to clients.

Example:

```text
Windows Server 2022
```

---

## DHCP Client

A DHCP Client is any device configured to obtain an IP address automatically.

Examples:

- Windows PC
- Laptop
- Server
- Printer

---

# DHCP Authorization

## What is DHCP Authorization?

In an Active Directory environment, a DHCP Server must be **authorized** before it can lease IP addresses to clients.

Authorization prevents unauthorized or rogue DHCP servers from distributing incorrect IP addresses.

Only Domain Administrators or Enterprise Administrators can authorize a DHCP Server.

---

# How to Authorize a DHCP Server

### Steps

1. Open **DHCP Manager**.
2. Expand the server.
3. Right-click the DHCP server.
4. Click **Authorize**.
5. Wait a few moments.
6. Refresh the DHCP console.

A green arrow on the server icon indicates that the DHCP server has been successfully authorized.

---

# DHCP Scope

## What is a Scope?

A **Scope** is a range of IP addresses that the DHCP server can assign to clients.

The scope also includes network configuration such as:

- Subnet Mask
- Default Gateway
- DNS Server
- Lease Duration

---

### Example Scope

```text
Start IP

192.168.1.100

End IP

192.168.1.200

Subnet Mask

255.255.255.0

Gateway

192.168.1.1

DNS

192.168.1.10
```

Clients receive addresses only from this range.

---

# Scope Components

A DHCP Scope includes:

- Scope Name
- IP Address Range
- Subnet Mask
- Exclusion Range
- Lease Duration
- Default Gateway
- DNS Server

---

# DHCP DORA Process

The DORA process is the communication between a DHCP Client and a DHCP Server.

It consists of four steps.

---

## D - Discover

The client broadcasts a **DHCP Discover** message to locate available DHCP servers.

```text
Client

↓

DHCP Discover
```

---

## O - Offer

The DHCP Server responds with an available IP address.

```text
DHCP Server

↓

DHCP Offer
```

---

## R - Request

The client requests the offered IP address.

```text
Client

↓

DHCP Request
```

---

## A - Acknowledge

The DHCP Server confirms the request and leases the IP address.

```text
DHCP Server

↓

DHCP ACK
```

---

# DORA Flow Diagram

```text
Client                       DHCP Server

DHCP Discover  ------------->

              <-------------  DHCP Offer

DHCP Request   ------------->

              <-------------  DHCP ACK
```

After the ACK message, the client receives its IP configuration and joins the network.

---

# DHCP Lease

A DHCP lease is the amount of time a client can use an assigned IP address before it must renew it.

Example:

```
Lease Time = 8 Days
```

---

# DHCP Lease Renewal Process

A client automatically renews its lease before it expires.

### Example

Assume:

```text
Lease Time = 8 Days
```

- Day 0 – Client receives IP address.
- Day 4 (50% of lease time) – Client contacts the DHCP server directly to renew the lease.
- If the server responds, the lease is renewed and the timer resets.
- If there is no response, the client retries later (around 87.5% of the lease time).
- If the lease expires without renewal, the client stops using the IP address and starts the DORA process again.

This automatic renewal ensures uninterrupted network connectivity.

---

# Lab Requirement

For this lab, I used:

| System | Purpose |
|---------|---------|
| DC01 | Windows Server with DHCP Role |
| Client01 | Windows Client configured for automatic IP assignment |

Both systems were connected to the same network.

---

# Installing the DHCP Role

### Steps

1. Open **Server Manager**.
2. Click **Manage**.
3. Select **Add Roles and Features**.
4. Choose **Role-based or feature-based installation**.
5. Select the local server.
6. Select **DHCP Server**.
7. Click **Add Features**.
8. Click **Next**.
9. Click **Install**.
10. Wait for the installation to complete.

---

# Completing DHCP Post-Installation

After installation:

1. Click the **Notification** flag in Server Manager.
2. Select **Complete DHCP Configuration**.
3. Click **Next**.
4. Choose the appropriate credentials (usually Domain Administrator).
5. Click **Commit**.
6. Click **Close**.

The DHCP server is now ready for configuration.

---

# Creating a DHCP Scope

### Steps

1. Open **DHCP Manager** (`dhcpmgmt.msc`).
2. Expand the server.
3. Expand **IPv4**.
4. Right-click **IPv4**.
5. Select **New Scope**.
6. Click **Next**.
7. Enter a Scope Name.
8. Specify the Start and End IP Address.
9. Enter the Subnet Mask.
10. Configure any Exclusion Range if required.
11. Set the Lease Duration.
12. Configure the Default Gateway.
13. Configure the DNS Server.
14. Click **Finish**.
15. Right-click the new scope.
16. Select **Activate**.

---

# Configuring the Client

On the Windows client:

1. Open **Network Connections**.
2. Open the network adapter properties.
3. Select **Internet Protocol Version 4 (TCP/IPv4)**.
4. Click **Properties**.
5. Select:
   - **Obtain an IP address automatically**
   - **Obtain DNS server address automatically**
6. Click **OK**.

---

# Verifying DHCP

Open Command Prompt on the client:

Display the assigned IP address:

```cmd
ipconfig
```

Release the current lease:

```cmd
ipconfig /release
```

Request a new lease:

```cmd
ipconfig /renew
```

Display complete network information:

```cmd
ipconfig /all
```

The client should receive an IP address from the configured DHCP scope.

---

# Common DHCP Issues

- DHCP Server not authorized.
- Scope not activated.
- IP address pool exhausted.
- Client configured with a static IP address.
- Firewall blocking DHCP traffic.
- Incorrect DNS or Gateway configuration.
- Network connectivity problems.

---

# Troubleshooting DHCP

Verify the client's IP configuration:

```cmd
ipconfig /all
```

Release the current lease:

```cmd
ipconfig /release
```

Renew the lease:

```cmd
ipconfig /renew
```

Test network connectivity:

```cmd
ping <DHCP Server IP>
```

Check the DHCP Server console to ensure:
- The server is authorized.
- The scope is active.
- Available IP addresses remain in the scope.

---

# What I Learned

In this lab, I installed and configured the DHCP Server role on Windows Server, authorized the server in Active Directory, created and activated a DHCP scope, configured client computers to obtain IP addresses automatically, and verified IP assignment using Windows networking commands. I also learned the DORA process, DHCP lease renewal, and common troubleshooting steps used to diagnose DHCP-related issues.
````
