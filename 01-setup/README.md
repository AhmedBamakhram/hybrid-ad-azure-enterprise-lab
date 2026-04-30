## Lab Environment Setup

### Virtualization Platform
- Used VMware Workstation Pro (version 25H2u1)
- Selected for stability, performance, and reliable networking for lab environments

### System Requirements
- Host Machine: Windows 10/11
- RAM: Minimum 16 GB (recommended 32 GB)
- Storage: SSD with at least 100 GB free space

### Virtual Machines Created
- Domain Controller (Windows Server 2022)
- Client Machine (Windows 10/11)

### Operating Systems
- Windows Server 2016 (for infrastructure services)
- Windows 10/11 (client device)

### Server Roles & Services
- Active Directory Domain Services (AD DS)
- DNS (Domain Name System)
- DHCP (Dynamic Host Configuration Protocol)
- Group Policy Management
- File Server (File Sharing)
- Print Server
- Windows Firewall Configuration
- Backup and Restore (Windows Server Backup)

### Network Configuration
- Configured internal virtual network
- Assigned static IP address to Domain Controller
- Configured DNS to point to Domain Controller
- Verified connectivity between virtual machines

### Tools & Software
- VMware Workstation Pro
- Windows Server 2022 ISO
- Windows 10/11 ISO

### Validation
- Verified VM network connectivity (ping test)
- Confirmed DNS name resolution
- Validated client communication with Domain Controller
