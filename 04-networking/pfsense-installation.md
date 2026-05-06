# 15 - Install and Configure pfSense Firewall

## Overview
pfSense Community Edition was installed on VMware Workstation and configured as the primary firewall and gateway for the lab environment.

pfSense replaces RRAS for routing and firewall services.  
DC01 continues to provide **Active Directory, DNS, and DHCP**.

---

## Lab Design

| Component | Role |
|----------|------|
| pfSense | Firewall, gateway, routing, NAT |
| DC01 | Active Directory, DNS, DHCP |
| VMware VMnets | Simulated VLAN networks |
| Windows Client | Connectivity and DHCP testing |

---

## VLAN / VMnet Design

| VMnet | VLAN Name | Network | Purpose |
|-------|-----------|---------|---------|
| VMnet1 | IT | 10.10.10.0/24 | Domain Controller + IT systems |
| VMnet2 | HR | 10.10.20.0/24 | HR department |
| VMnet3 | Finance | 10.10.30.0/24 | Finance systems |
| VMnet4 | Guest | 10.10.40.0/24 | Guest access |
| VMnet5 | Public | 10.10.50.0/24 | Public-facing services |
| VMnet8 | WAN | 192.168.88.0/24 | VMware NAT / Internet |

---

## pfSense VM Hardware

| Setting | Value |
|--------|--------|
| VM Name | pfSense |
| OS Type | FreeBSD 64-bit |
| CPU | 2 cores |
| Memory | 2 GB |
| Disk | 20 GB |
| Network Adapter 1 | VMnet8 (WAN) |
| Network Adapter 2 | VMnet1 (LAN) |

---

## Step 1 - Create pfSense VM

1. Open VMware Workstation Pro.
2. File → **New Virtual Machine**
3. Select **Typical**.
4. Choose pfSense ISO:

netgate-installer-v1.2-RELEASE-amd64.iso

5. OS Type: **Other → FreeBSD 64-bit**
6. VM Name: **pfSense**
7. Disk Size: **20 GB**
8. Customize Hardware:
- Memory: **2 GB**
- CPU: **2 cores**

---

## Step 2 - Configure Network Adapters

| Adapter | VMware Network | pfSense Role |
|---------|----------------|--------------|
| Network Adapter 1 | VMnet8 | WAN |
| Network Adapter 2 | VMnet1 | LAN |

**WAN = VMnet8 (NAT)**  
**LAN = VMnet1 (IT network)**

---

## Step 3 - Install pfSense CE

1. Power on the VM.
2. Select **Install pfSense CE**.
3. Accept defaults.
4. Confirm disk installation.
5. After installation:
- Remove ISO  
  *VM Settings → CD/DVD → Uncheck “Connect at power on”*
6. Reboot.

---

## Step 4 - Assign pfSense Interfaces

| pfSense Interface | Adapter | Purpose |
|------------------|---------|---------|
| WAN | em0 | Internet / VMnet8 |
| LAN | em1 | IT LAN / VMnet1 |

Final mapping:

WAN → em0
LAN → em1


---

## Step 5 - Configure LAN IP

Set LAN interface:


---

## Step 5 - Configure LAN IP

Set LAN interface:

IP Address: 10.10.10.254
Subnet Mask: 255.255.255.0
DHCP Server: Disabled
WebConfigurator: HTTPS


DHCP is handled by **DC01**, not pfSense.

---

## Step 6 - Access pfSense Web GUI

From a client on VMnet1:


DHCP is handled by **DC01**, not pfSense.

---

## Step 6 - Access pfSense Web GUI

From a client on VMnet1:

https://10.10.10.254


Default login:

Username: admin
Password: pfsense


---

## Step 7 - pfSense Setup Wizard

| Setting | Value |
|---------|--------|
| Hostname | pfsense |
| Domain | lab.local |
| Primary DNS | 10.10.10.10 |
| Time Server | 10.10.10.10 |
| Timezone | America/Toronto |
| WAN Type | DHCP |
| LAN IP | 10.10.10.254 |

Change the default admin password.

---

## Step 8 - Verify WAN

Navigate to:

**Status → Interfaces**

Expected:

WAN IP: 192.168.88.x
Gateway: 192.168.88.2
Status: Up

---

## Step 9 - Verify Internet Access

Diagnostics → **Ping**

Test:8.8.8.8

Expected:0% packet loss


---

## Step 10 - Verify NAT

Firewall → **NAT → Outbound**

Mode: Automatic outbound NAT rule generation


Expected rule:
Source: 10.10.10.0/24
Translation: WAN address


---

## Step 11 - Verify LAN Firewall Rule

Firewall → **Rules → LAN**

Default rule should exist: IPv4 LAN net → any


---

## Step 12 - Disable RRAS on DC01

1. Server Manager → Tools → Routing and Remote Access
2. Right‑click DC01
3. Select **Disable Routing and Remote Access**

Expected:
RRAS disabled
pfSense now handles routing


---

## Step 13 - Configure DC01 Static IP

Network Adapter (IT):
IP Address:      10.10.10.10
Subnet Mask:     255.255.255.0
Default Gateway: 10.10.10.254
DNS Server:      10.10.10.10


Important:
- **Only the IT adapter** should have a default gateway.

---

## Step 14 - Update DHCP Scope Options

DHCP → IPv4 → Scope → **Scope Options**

Update: 003 Router = 10.10.10.254


### DHCP Gateway Plan

| VLAN | Network | Gateway (Option 003) |
|------|----------|----------------------|
| IT | 10.10.10.0/24 | 10.10.10.254 |
| HR | 10.10.20.0/24 | 10.10.20.254 |
| Finance | 10.10.30.0/24 | 10.10.30.254 |
| Guest | 10.10.40.0/24 | 10.10.40.254 |
| Public | 10.10.50.0/24 | 10.10.50.254 |

---

## Step 15 - Test DC01 Connectivity
ping 10.10.10.254
ping 8.8.8.8


Expected:
Reply from pfSense
Reply from internet


---

## Step 16 - Test Client DHCP
ipconfig /release
ipconfig /renew
ipconfig /all


Expected:
IP: 10.10.10.x
Gateway: 10.10.10.254
DNS: 10.10.10.10
DHCP: 10.10.10.10


---

## Step 17 - Test Client Connectivity
ping 10.10.10.254   (pfSense)
ping 10.10.10.10    (DC01)
ping 8.8.8.8        (Internet)


---

## Final Architecture

Internet
|
VMware NAT (VMnet8)
|
pfSense WAN
pfSense LAN: 10.10.10.254
|
VMnet1 / IT Network
|
DC01 (10.10.10.10)
|
Windows Clients


---

## Key Design Decision

RRAS was used initially for routing tests.  
pfSense was later introduced as the **dedicated enterprise firewall**.

Final roles:
- **pfSense** = Routing, firewall, NAT  
- **DC01** = AD, DNS, DHCP  
- **Clients** = DHCP from DC01, gateway = pfSense  

---

## Snapshot

**Name:**  
pfSense Installed - Firewall and Gateway Configured


**Description:**  
pfSense CE installed and configured as the main firewall. WAN via VMnet8, LAN via VMnet1 (10.10.10.254). RRAS disabled on DC01. DHCP Option 003 updated to point to pfSense.

---

## Troubleshooting Notes

### pfSense can ping internet but DC01 cannot
- Check DC01 gateway: 10.10.10.254

- Ensure only one default gateway exists.

### Client receives no gateway
- Verify DHCP Option 003: 10.10.10.254


### pfSense Web GUI not loading
- Ensure client is on VMnet1.
- Test: ping 10.10.10.254

- 
### WAN has no internet
Check:
- Status → Interfaces  
- Firewall → NAT → Outbound  
- Firewall → Rules → LAN  
- Diagnostics → Ping  




