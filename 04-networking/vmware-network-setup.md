# VMware Network Setup (Simulated VLANs)

## Overview

This lab simulates enterprise VLAN segmentation using VMware Workstation Host-only networks.  
Since VMware Workstation does not support native VLAN tagging (802.1Q), each VLAN is represented using a separate VMnet network.

This design provides logical network isolation similar to real-world VLAN environments.

---

## Network Design

| VMnet | VLAN Name | Network | Purpose |
|------|----------|--------|--------|
| VMnet1 | IT | 10.10.10.0/24 | Domain Controller & core IT systems |
| VMnet2 | HR | 10.10.20.0/24 | Human Resources department |
| VMnet3 | Finance | 10.10.30.0/24 | Financial systems |
| VMnet4 | Guest | 10.10.40.0/24 | Guest access (isolated) |
| VMnet5 | Public | 10.10.50.0/24 | Public-facing services |

---

## Create Networks in VMware

### 1. Open Virtual Network Editor

Open VMware Workstation Pro:

```plaintext
Edit → Virtual Network Editor

---

## Notes

- VMware Workstation does not support native VLAN tagging (802.1Q)
- VLAN segmentation is simulated using separate VMnet networks
- Each VMnet functions as an isolated Layer 2 network
- Inter-network communication is restricted by default
- Routing between VLANs will be implemented using a routing solution (e.g., RRAS or pfSense)
