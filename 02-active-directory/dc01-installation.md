# Windows Server 2022 Installation (DC01) - VMware

## Overview
This section documents the process of creating and installing a Windows Server 2022 virtual machine (DC01) using VMware Workstation Pro.

---

## Virtual Machine Creation

### 1. Create New VM
- Open VMware Workstation Pro
- Select: **Create a New Virtual Machine**
- Choose: **Typical (Recommended)**

### 2. Installation Method
- Select: **I will install the operating system later**
  - (Avoids VMware Easy Install issues)

### 3. Guest Operating System
- OS: Microsoft Windows
- Version: Windows Server 2022

### 4. VM Name and Location
- Name: `DC01`
- Location: `D:\VMs\DC01\` (or `C:\VMs\DC01\`)

---

## Hardware Configuration

### CPU
- 2 processors

### Memory
- 4 GB (minimum recommended)

### Hard Disk
- Size: 60 GB
- Disk Type: **NVMe (Recommended)**
- Store as a single file

### Network Adapter
- Custom: **VMnet1 (Host-only)**

---

## Important Pre-Installation Configuration

### Remove Floppy Drive
- VM Settings → Floppy → Remove  
- (Prevents installation errors)

### Configure CD/DVD
- Use ISO image file (Windows Server 2022 ISO)
- Enable:
  - Connected
  - Connect at power on
- Set connection type: **IDE**  
  (Improves compatibility during installation)

---

## Installation Steps

### 1. Start VM
- Power on virtual machine
- Press **ESC** to open boot menu
- Select: **CD/DVD Drive**

### 2. Boot from ISO
- Press any key when prompted:
  - “Press any key to boot from CD/DVD”

### 3. Windows Setup
- Select language and keyboard → Next
- Click: Install Now

### 4. Product Key
- Select: **I don’t have a product key**

### 5. Edition Selection
- Choose:
  **Windows Server 2022 Standard Evaluation (Desktop Experience)**

### 6. Disk Selection
- Select virtual disk → Next

### 7. Installation
- Wait for installation to complete

### 8. Administrator Setup
- Set Administrator password
- Log in to system

---

## Notes

- ISO must be complete (~5.5 GB) to avoid installation errors
- CD/DVD should use IDE during installation to prevent compatibility issues
- Floppy drive should be removed to avoid boot and setup errors

---

## Outcome

A clean Windows Server 2022 virtual machine (DC01) is successfully installed and ready for further configuration (networking, static IP, Active Directory setup).
