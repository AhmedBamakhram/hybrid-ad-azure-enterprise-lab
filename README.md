# Hybrid AD & Azure Enterprise Lab

## Overview
This project demonstrates the design and implementation of a hybrid enterprise IT environment combining on-premises infrastructure with Microsoft Azure services.

The lab simulates a real-world corporate network including Active Directory, Group Policy, networking services, Azure AD (Entra ID), Microsoft Intune, and security configurations.

---

## Architecture
![Network Diagram](architecture/network-diagram.png)


---

## Key Components

- Active Directory Domain Services (AD DS)
- Group Policy Management
- DNS & DHCP Configuration
- File and Print Services
- Hybrid Identity Integration with Microsoft Entra ID
- Microsoft Intune (Endpoint Management)
- Multi-Factor Authentication (MFA)
- Conditional Access Policies
- PowerShell Automation
- Inter-VLAN Routing and Network Segmentation
- pfSense Firewall and Routing
- VMware Virtual Networking
- Remote Access and VPN Configuration
- Windows Server Administration
- Infrastructure Monitoring and Troubleshooting

---

## Lab Structure

- `01-setup` → Environment setup and VMware configuration
- `02-active-directory` → AD DS installation and management
- `03-group-policy` → Security baselines and policy management
- `04-networking` → DNS, DHCP, VLANs, RRAS, and pfSense setup
- `05-azure` → Microsoft Entra ID and cloud integration
- `06-intune` → Device management and compliance policies
- `07-security` → MFA, Conditional Access, and security hardening
- `08-automation` → PowerShell scripting and automation
- `09-scenarios` → Real-world troubleshooting and support scenarios

---

## Scenarios Implemented

- User login and authentication troubleshooting
- Group Policy deployment issues
- DNS resolution and DHCP troubleshooting
- Azure AD Connect synchronization issues
- Intune device compliance troubleshooting
- VPN connectivity troubleshooting
- Inter-VLAN routing configuration
- Network isolation and firewall rule testing
- pfSense firewall and gateway configuration
- Client-to-server communication troubleshooting
- Internet connectivity troubleshooting across VLANs
- Active Directory user and permissions management

---
## Technologies Used

- Windows Server 2025
- Windows 10/11
- VMware Workstation Pro
- Microsoft Azure
- Microsoft Entra ID
- Microsoft Intune
- pfSense Firewall
- PowerShell
- Active Directory Domain Services (AD DS)
- DNS / DHCP
- RRAS (Routing and Remote Access Service)
- VLAN Segmentation
- Virtual Networking
---

## Author

Ahmed Bamakhram
