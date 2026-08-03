# Windows Server Installation
# Windows Server Lab Setup

To build this Windows Server Administration lab, I first installed a virtualization platform on my laptop. I used Oracle VirtualBox (VMware Workstation can also be used) to create a virtual environment where multiple operating systems could run simultaneously. This allowed me to simulate an enterprise network without requiring multiple physical computers.

During the installation of the virtualization software, Windows prompted me to install virtual network adapters and required drivers. I allowed all the necessary permissions because these components are essential for virtual machine networking and communication.

After setting up the virtualization software, I downloaded the Windows Server 2022 Evaluation ISO from Microsoft. Windows Server 2025 can also be used for the same lab. I stored the ISO file in a dedicated folder on my local system so it could be reused whenever I needed to create additional virtual machines.

Next, I created the virtual machines required for the lab environment. The primary server was configured to act as the Domain Controller, while additional virtual machines were created to function as Windows clients. As the project progressed, I also created another Windows Server virtual machine to configure an Additional Domain Controller for redundancy and replication.

While creating each virtual machine, I allocated the required hardware resources such as CPU, RAM, and storage based on the available resources of my host computer. I also selected the Windows Server ISO as the bootable installation media and stored all virtual machine files in a separate directory to keep the lab organized.

# Example Configuration
Operating System: Windows Server 2022 Evaluation
Processor: 2 Virtual CPUs
Memory: 4 GB RAM
Storage: 60 GB Virtual Disk
ISO Location: D:\ISO\Windows_Server_2022.iso
VM Location: D:\Virtual Machines\

Once the virtual machines were created, I installed the operating systems and completed the initial Windows Server setup before moving on to the server configuration.

# Network Topology

To ensure proper communication between all systems, I connected every virtual machine to the same virtual network using the virtualization platform. This allowed the Domain Controller and client systems to communicate with each other throughout the lab.

The Domain Controller acts as the central server for the environment and provides services such as Active Directory Domain Services (AD DS), DNS, DHCP, authentication, and Group Policy. All Windows clients connect to this server and become members of the domain.

                     Host Computer
                           │
          Oracle VirtualBox / VMware Workstation
                           │
                Virtual Network (Same Network)
       ┌────────────────┬────────────────┬───────────────┐
       │                │                │
       ▼                ▼                ▼
Domain Controller     Client-01       Client-02
Windows Server       Windows 11      Windows 11
       │
       ├── Active Directory (AD DS)
       ├── DNS Server
       ├── DHCP Server
       ├── Group Policy
       └── File Services

This virtual environment became the foundation for the rest of the project, where I configured Active Directory, DNS, DHCP, Group Policy, user and computer management, file services, permissions, backup, and other Windows Server administration tasks documented throughout this repository.
