# Active Directory (AD)
# What is Active Directory?

Active Directory (AD) is a service in Windows Server that helps manage users, computers, groups, and other network resources from one central place. Instead of configuring every computer one by one, an administrator can manage everything from a single server.

For example, if a company has 100 computers, there is no need to create user accounts or change settings on each computer separately. Active Directory makes this work much easier by allowing everything to be managed from the Domain Controller.

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

# Active Directory Database (NTDS.DIT)

The Active Directory database stores all the information about the domain, such as users, computers, groups, Organizational Units (OUs), and security settings. This database is used by the Domain Controller to authenticate users and manage Active Directory.

The database file is called NTDS.DIT (NT Directory Services Directory Information Tree). By default, it is stored in the following location:

C:\Windows\NTDS\NTDS.dit

This file is one of the most important components of Active Directory and should be protected and backed up regularly because it contains all the domain information.

# Installing Active Directory Domain Services (AD DS)

After completing the basic server configuration, I installed the Active Directory Domain Services (AD DS) role using Server Manager.

Steps
Open Server Manager.
Click Manage and select Add Roles and Features.
Click Next until you reach Server Roles.
Select Active Directory Domain Services (AD DS).
When prompted, click Add Features to install the required management tools.
Click Next and continue with the default settings.
Click Install and wait for the installation to complete.
Once the installation is finished, click Close.

After installing the AD DS role, the server is not yet a Domain Controller. The next step is to promote the server to a Domain Controller, where a new domain or an existing domain can be configured.

# Promoting the Server to a Domain Controller

After installing the AD DS role, the next step was to promote the server to a Domain Controller.

Steps
Open Server Manager.
Click the Notification flag at the top right.
Select Promote this server to a domain controller.
Choose Add a new forest (for a new environment).
Enter the Root Domain Name (for example, company.local).
Click Next.
Select the Forest Functional Level and Domain Functional Level.
Set the Directory Services Restore Mode (DSRM) password.
Click Next through the remaining configuration pages.
Review the settings and click Install.
The server will automatically restart after the installation is complete.

After the restart, the Windows Server becomes a Domain Controller, and the new Active Directory domain is created. From this point, the server is ready to manage users, computers, groups, and other Active Directory resources.

Verification

After logging in, I verified that the Domain Controller was working correctly by opening:

Active Directory Users and Computers (ADUC)
Active Directory Administrative Center (ADAC)
DNS Manager
Group Policy Management Console (GPMC)

I also confirmed that the server was using the newly created domain and that all Active Directory services were running successfully.
