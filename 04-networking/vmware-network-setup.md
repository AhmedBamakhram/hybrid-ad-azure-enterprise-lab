# VMware Network Setup (Simulated VLANs)

## Overview

This lab simulates VLAN segmentation using VMware Workstation Host-only networks.  
Each VMnet represents a separate VLAN with its own subnet.

---

## Network Design

| VMnet | VLAN Name | Network | Purpose |
|------|----------|--------|--------|
| VMnet1 | IT | 10.10.10.0/24 | Domain Controller & IT systems |
| VMnet2 | HR | 10.10.20.0/24 | HR department |
| VMnet3 | Finance | 10.10.30.0/24 | Financial systems |
| VMnet4 | Guest | 10.10.40.0/24 | Guest access (isolated) |
| VMnet5 | Public | 10.10.50.0/24 | Public-facing services |

---

## Create Networks in VMware

Open:

```plaintext
Edit → Virtual Network Editor

## Notes

- VMware Workstation does not support native VLAN tagging (802.1Q)
- VLANs are simulated using separate VMnet networks
- Each VMnet represents an isolated network segment by default
- Inter-VLAN communication is not available until routing is configured
- Routing between VLANs will be implemented in a later phase of the lab

