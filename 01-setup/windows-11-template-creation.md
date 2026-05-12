# Windows 11 Template Creation and VM Cloning

## Overview

This section documents the creation of a standardized Windows 11 client template and the cloning process used to deploy multiple enterprise client virtual machines in the Hybrid AD & Azure Enterprise Lab.

---

# Windows 11 Template Creation

## Virtual Machine Specifications

| Setting | Configuration |
|---|---|
| Operating System | Windows 11 Pro |
| RAM | 4 GB |
| CPU | 2 vCPUs |
| Disk Size | 60 GB |
| Disk Type | NVMe |
| Firmware | UEFI |
| TPM | Enabled |
| Network Adapter | VMnet1 |
| Virtualization Platform | VMware Workstation Pro |

---

## VM Creation Steps

1. Open VMware Workstation Pro
2. Create a new virtual machine
3. Select:
   - Typical (recommended)
4. Choose:
   - I will install the operating system later
5. Select:
   - Microsoft Windows
   - Windows 11 x64
6. Configure VM specifications
7. Enable UEFI and TPM
8. Mount Windows 11 ISO
9. Install Windows 11 Pro
10. Install VMware Tools
11. Run Windows Updates
12. Shutdown VM

---

## Template VM Name

```text
WIN11-TEMPLATE
```

---

## VMware Tools Installation

1. Power on VM
2. In VMware menu:
   - VM → Install VMware Tools
3. Open:
   - This PC
4. Open VMware Tools DVD
5. Run:
   - setup64.exe
6. Choose:
   - Typical Installation
7. Restart VM

---

## Snapshot Creation

After completing the Windows installation and updates:

1. Shutdown VM
2. Right-click VM
3. Select:
   - Snapshot → Take Snapshot

Snapshot Name:

```text
Clean-Win11-Template
```

---

# VM Cloning Process

## Overview

The Windows 11 template was cloned to create multiple department client systems for the enterprise lab environment.

---

## Clone Type

Because Windows 11 uses TPM and encryption, full clones were used.

| Clone Type | Usage |
|---|---|
| Full Clone | Used |
| Linked Clone | Not supported with encrypted TPM VMs |

---

## Cloning Steps

1. Right-click:
   - WIN11-TEMPLATE
2. Select:
   - Manage → Clone
3. Choose:
   - Existing Snapshot
4. Select:
   - Clean-Win11-Template
5. Choose:
   - Create a Full Clone
6. Configure VM name and location
7. Click:
   - Finish

---

# Virtual Machines Created

| VM Name | Department | Network |
|---|---|---|
| IT-PC01 | IT | VMnet1 |
| HR-PC01 | Human Resources | VMnet2 |
| FIN-PC01 | Finance | VMnet3 |
| GUEST-PC01 | Guest Network | VMnet4 |

---

# VM Folder Structure

```text
D:\VMs\IT-PC01
D:\VMs\HR-PC01
D:\VMs\FIN-PC01
D:\VMs\GUEST-PC01
```

---

# Network Assignment

Each VM was connected to a dedicated VMware virtual network.

| Department | VMnet | Subnet |
|---|---|---|
| IT | VMnet1 | 10.10.10.0/24 |
| HR | VMnet2 | 10.10.20.0/24 |
| Finance | VMnet3 | 10.10.30.0/24 |
| Guest | VMnet4 | 10.10.40.0/24 |

---

# Post-Cloning Tasks

After cloning:

1. Power on one VM at a time
2. Rename computer
3. Restart VM
4. Verify DHCP assignment
5. Join domain (except Guest)

---

# Domain Membership

| VM Name | Domain Joined |
|---|---|
| IT-PC01 | Yes |
| HR-PC01 | Yes |
| FIN-PC01 | Yes |
| GUEST-PC01 | No |

Domain:

```text
lab.local
```

---

# DHCP Relay Configuration

Because DHCP server (DC01) resides on the IT subnet, DHCP Relay was configured on pfSense to allow other VLANs/subnets to obtain IP addresses.

## DHCP Server

```text
10.10.10.10
```

## pfSense DHCP Relay Interfaces

- HR
- Finance
- Guest
- Public

---

# VMware Lock File Troubleshooting

During cloning operations, VMware lock file issues occurred.

## Symptoms

```text
This virtual machine appears to be in use
```

## Resolution Steps

1. Close VMware Workstation
2. End:
   - VMware Workstation VMX processes
3. Navigate to VM folder
4. Delete:
   - *.lck folders/files
5. Reopen VMware

---

# Result

Successfully deployed a segmented enterprise lab environment with multiple department workstations connected through pfSense routing and Active Directory infrastructure.
