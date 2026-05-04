# DC01 Network Configuration (Multi-NIC Setup)

## Overview

This section documents the configuration of multiple network interfaces on the Domain Controller (DC01) to support simulated VLAN segmentation in VMware Workstation.

DC01 is connected to five separate VMnet networks, each representing a different VLAN.

---

## Add Network Adapters (VMware)

1. Power off DC01 virtual machine

2. In VMware Workstation:
   
   - Right-click **DC01**
   - Select **Settings**

3. Add additional network adapters:

   - Click **Add...**
   - Select **Network Adapter**
   - Click **Finish**

4. Repeat the process until a total of **5 network adapters** are present

---

## Assign VMnet Networks

Configure each adapter as follows:

| Adapter | VMnet | VLAN |
|--------|------|------|
| Network Adapter 1 | VMnet1 | IT |
| Network Adapter 2 | VMnet2 | HR |
| Network Adapter 3 | VMnet3 | Finance |
| Network Adapter 4 | VMnet4 | Guest |
| Network Adapter 5 | VMnet5 | Public |

For each adapter:

- Select **Custom: Specific virtual network**
- Choose the appropriate VMnet
- Ensure:
  - ✔ Connected
  - ✔ Connect at power on

---

## Verify Network Adapters in Windows

1. Start DC01

2. Open Network Connections:

```plaintext
ncpa.cpl
```
## Rename Network Adapters

After confirming that five network adapters are available in Windows, rename each adapter to match its VLAN purpose.

This makes the configuration easier to manage and prevents confusion when assigning IP addresses.

| Original Name | New Name | Purpose |
|--------------|----------|---------|
| Ethernet1 | IT | Domain Controller & IT systems |
| Ethernet2 | HR | HR VLAN |
| Ethernet3 | Finance | Finance VLAN |
| Ethernet4 | Guest | Guest VLAN |
| Ethernet5 | Public | Public services VLAN |
