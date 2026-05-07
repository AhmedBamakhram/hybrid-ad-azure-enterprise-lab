# 16 — pfSense Inter‑VLAN Routing and Firewall Rules

## Overview
pfSense was expanded from a basic WAN/LAN firewall into a full multi-interface router/firewall for all lab networks.  
Additional VMware network adapters were added for HR, Finance, Guest, and Public networks.  
Each interface received a static gateway IP, and firewall rules were created to control inter‑VLAN traffic.

---

## Network Design

| VMnet  | VLAN Name | Network        | pfSense Gateway |
|--------|-----------|----------------|-----------------|
| VMnet1 | IT        | 10.10.10.0/24  | 10.10.10.254    |
| VMnet2 | HR        | 10.10.20.0/24  | 10.10.20.254    |
| VMnet3 | Finance   | 10.10.30.0/24  | 10.10.30.254    |
| VMnet4 | Guest     | 10.10.40.0/24  | 10.10.40.254    |
| VMnet5 | Public    | 10.10.50.0/24  | 10.10.50.254    |
| VMnet8 | WAN       | 192.168.88.0/24 (DHCP) |

---

## Step 1 — Add Network Adapters to pfSense (VMware)

Power off pfSense → open **Settings** → add adapters:

| Adapter | VMnet  | Purpose          |
|---------|--------|------------------|
| 1       | VMnet8 | WAN / Internet   |
| 2       | VMnet1 | IT / LAN         |
| 3       | VMnet2 | HR               |
| 4       | VMnet3 | Finance          |
| 5       | VMnet4 | Guest            |
| 6       | VMnet5 | Public           |

Enable:
- Connected  
- Connect at power on  
- Custom: Specific VMnet  

---

## Step 2 — Assign Interfaces (pfSense Console)

Console → **1) Assign Interfaces**

When asked *“Should VLANs be set up now?”* → `n`

Assign:

| pfSense Interface | NIC | Network          |
|-------------------|-----|------------------|
| WAN               | em0 | VMnet8           |
| LAN               | em1 | VMnet1 / IT      |
| OPT1              | em2 | VMnet2 / HR      |
| OPT2              | em3 | VMnet3 / Finance |
| OPT3              | em4 | VMnet4 / Guest   |
| OPT4              | em5 | VMnet5 / Public  |

Proceed → `y`

---

## Step 3 — Configure Interface IPs (Console)

Console → **2) Set interface(s) IP address**

### HR (OPT1)
- IPv4: `10.10.20.254`
- Subnet: `/24`
- Gateway: *none*
- DHCP: n  
- WebConfigurator: n  

### Finance (OPT2)
- IPv4: `10.10.30.254`
- Subnet: `/24`
- Gateway: *none*

### Guest (OPT3)
- IPv4: `10.10.40.254`
- Subnet: `/24`

### Public (OPT4)
- IPv4: `10.10.50.254`
- Subnet: `/24`

---

## Step 4 — Rename Interfaces (pfSense GUI)

Open: `https://10.10.10.254`

Interfaces → rename:

| Original | New Name |
|----------|----------|
| OPT1     | HR       |
| OPT2     | Finance  |
| OPT3     | Guest    |
| OPT4     | Public   |

Verify:

| Interface | IPv4 Address     |
|-----------|------------------|
| HR        | 10.10.20.254/24  |
| Finance   | 10.10.30.254/24  |
| Guest     | 10.10.40.254/24  |
| Public    | 10.10.50.254/24  |

Save → Apply

---

## Step 5 — Update DHCP Scope Options (DC01)

DHCP → Scope Options → **003 Router**

| Scope   | Router (003)     |
|---------|-------------------|
| IT      | 10.10.10.254      |
| HR      | 10.10.20.254      |
| Finance | 10.10.30.254      |
| Guest   | 10.10.40.254      |
| Public  | 10.10.50.254      |

DNS (006): `10.10.10.10`

---

## Step 6 — Firewall Rule Design

| Network | Policy                                      |
|---------|----------------------------------------------|
| IT      | Full access                                  |
| HR      | Access to IT + Internet                      |
| Finance | Access to IT + Internet                      |
| Guest   | Internet only (no internal access)           |
| Public  | Future DMZ / hosted services                 |

---

## Step 7 — IT Firewall Rule

Firewall → Rules → **LAN**

Keep default: Pass | LAN net → any


---

## Step 8 — HR Firewall Rule

Firewall → Rules → **HR**
Action: Pass
Source: HR net
Destination: Any
Description: Allow HR to IT and Internet


Apply.

---

## Step 9 — Finance Firewall Rule

Firewall → Rules → **Finance**

Action: Pass
Source: Finance net
Destination: Any
Description: Allow Finance to IT and Internet


Apply.

---

## Step 10 — Guest Firewall Rules

Guest must reach Internet only.

Firewall → Rules → **Guest**

### Rule 1 — Block Guest → IT

Block | Guest net → LAN net

### Rule 2 — Block Guest → HR

Block | Guest net → HR net


### Rule 3 — Block Guest → Finance

Block | Guest net → Finance net


### Rule 4 — Allow Guest → Internet
Placed **below** block rules:

Pass | Guest net → Any
Description: Allow Guest Internet Access


Apply.

---

## Step 11 — Public Firewall Rule

Firewall → Rules → **Public**

Pass | Public net → Any
Description: Allow Public Internet Access

---

## Step 12 — Testing

### HR Client (VMnet2)
Expected:
- IP: `10.10.20.x`
- Gateway: `10.10.20.254`
- DNS: `10.10.10.10`

Test:
ping 10.10.20.254
ping 10.10.10.10
ping 8.8.8.8


### Finance Client (VMnet3)
Expected:
- IP: `10.10.30.x`
- Gateway: `10.10.30.254`

### Guest Client (VMnet4)
Expected:
- IP: `10.10.40.x`
- Gateway: `10.10.40.254`

Guest:
- Internet works  
- Internal networks blocked  

---

## Step 13 — Snapshot

**Name:** pfSense Inter‑VLAN Routing and Firewall Rules Configured  
**Description:** pfSense configured with IT, HR, Finance, Guest, Public interfaces, static gateways, DHCP updates, and firewall rules.

---


## Final Architecture

```text
Internet
   |
VMnet8 / WAN
   |
pfSense
   |
-------------------------------------------------
|        |          |           |               |
IT       HR         Finance     Guest           Public
VMnet1   VMnet2     VMnet3      VMnet4          VMnet5
10.10.10 10.10.20   10.10.30    10.10.40        10.10.50
```

