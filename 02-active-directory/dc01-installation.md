# Windows Server 2022 Installation (DC01) - VMware

## Overview
This section documents the process of creating and installing a Windows Server 2022 virtual machine (DC01) using VMware Workstation Pro.

---

## Virtual Machine Creation

### 1. Create New VM

![VM Setup](images/dc01-install-01-vm.png)

- Open VMware Workstation Pro
- Select: **Create a New Virtual Machine**
- Choose: **Typical (Recommended)**

### 2. Boot from ISO

![Boot Screen](images/dc01-install-02-boot.png)

- Power on virtual machine
- Press **ESC** to open boot menu
- Select: **CD/DVD Drive**

### 3. Windows Setup

![Setup Screen](images/dc01-install-03-setup.png)

- Select language and keyboard → Next
- Click: Install Now

### 4. Windows Installed

![Desktop](images/dc01-install-04-desktop.png)

- Windows Server installation completed
- Login with Administrator account

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

---

## Active Directory Installation

### 1. Add AD DS Role

![Deployment Config](images/dc01-ad-02-deployment-config.png)

- Open Server Manager
- Click **Add Roles and Features**
- Select **Active Directory Domain Services**

---

### 2. Configure Domain

![Domain Name](images/dc01-ad-03-domain-name.png)

- Select: **Add a new forest**
- Root domain name: `lab.local`

---

### 3. DNS Options

![DNS Options](images/dc01-ad-04-dns-options.png)

- Leave default settings
- Ignore delegation warning (normal in lab)

---

### 4. NetBIOS Name

![NetBIOS](images/dc01-ad-05-netbios.png)

- Confirm NetBIOS name: `LAB`

---

### 5. AD Paths

![Paths](images/dc01-ad-06-paths.png)

- Keep default paths:
  - `C:\Windows\NTDS`
  - `C:\Windows\SYSVOL`

---

### 6. Review Configuration

![Review](images/dc01-ad-07-Review Options.png)

- Review all settings before installation

---

### 7. Prerequisites Check

![Prereq Check](images/dc01-ad-08-prereq-check.png)

- Ensure all checks pass
- Ignore warnings if no critical errors

---

### 8. Domain Login

![Login](images/dc01-ad-09-login-domain.png)

- Server restarts after installation
- Login using:
  - `LAB\Administrator`

---

## Outcome

A fully configured Windows Server 2022 Domain Controller (DC01) with Active Directory Domain Services installed and ready for further configuration (Group Policy, users, domain join, etc.).
