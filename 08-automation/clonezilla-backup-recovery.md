# Clonezilla Backup and Bare-Metal Recovery

## Overview

Created a full disk backup of the SSD hosting the lab environment (including multiple virtual machines). This proactive approach ensures full system recovery in case of SSD failure.

## Tools Used

- Rufus (Portable x64)
- Clonezilla Live ISO
- USB flash drive
- External SSD

## Downloads

- Rufus: https://rufus.ie/en/
- Clonezilla ISO: https://clonezilla.org/downloads/download.php?branch=stable

---

## Creating Bootable Clonezilla USB

1. Open Rufus (Portable version – no installation required).
2. Click **Show advanced drive properties**.
3. Enable:

✔ List USB Hard Drives
4. Ensure your USB drive is detected.
5. Click **SELECT** and choose:

clonezilla-live-3.3.1-35-amd64.iso
6. Click **START**.

### When prompted:

- Select:

- Write in ISO Image mode (Recommended)
- 
- Click **Yes** when prompted to download bootloader files.
- Ensures proper boot compatibility
- Takes only a few seconds

- Click **OK** when warned:

ALL DATA ON USB WILL BE DELETED

### Notes

- Existing Windows installer partitions will be removed
- USB will be reformatted and made bootable

---

## Booting into Clonezilla

1. Insert:
 - Clonezilla USB
 - External SSD
2. Restart laptop
3. Open boot menu (F12 / ESC / F9)
4. Select USB device

---

## Backup Process (Disk Imaging)

1. Select: Clonezilla live (Default settings)
2. Language:English
3. Select:Keyboard
4.  Select: Keep default keyboard layout
5. Mode: Start Clonezilla
6. 7. Connect external SSD → press Enter
8. Select external SSD:local_dev
9. Mount:sdb (usually)
    10. Mode:
 ```
 Beginner
 ```
11. Operation:
 ```
 savedisk
 ```
12. Name backup:
 ```
 Laptop-Full-Backup-2026
 ```
13. Source disk:
 ```
 sda (internal SSD)
 ```
14. Compression:
 ```
 gzip (default)
 ```
15. Check option:
 ```
 Skip checking
 ```
16. Confirm:
 ```
 y → Enter
 y → Enter
 ```

---

## Backup Execution

- Clonezilla begins imaging the disk
- Duration depends on used data size
- Typical time: 20–60 minutes

---

## Recovery Process (SSD Failure Scenario)

If SSD fails:

1. Replace with new blank SSD
2. Insert Clonezilla USB + external SSD
3. Boot from USB
4. Select:/
5. Select: device-image
6. Choose backup location (external SSD)
7. Select:local_dev
   8. Choose backup image
9. Select new SSD as target
10. Confirm restore
11. Wait for completion
12. Restart system

---

## Outcome

- Full system image stored externally
- Supports complete recovery with no OS pre-installed
- Includes:
- Windows OS
- Applications
- Lab environment
- Virtual machines

---

## Skills Demonstrated

- Disk imaging (Clonezilla)
- Bare-metal recovery
- Bootable USB creation (Rufus)
- Disaster recovery planning
- Storage management
- Proactive infrastructure protection
- 
