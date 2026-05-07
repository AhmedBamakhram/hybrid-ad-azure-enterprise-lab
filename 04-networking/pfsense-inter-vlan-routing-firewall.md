# 16 - pfSense Inter-VLAN Routing and Firewall Rules

## Overview

In this step, pfSense was expanded from a basic WAN/LAN firewall into a multi-interface router/firewall for all lab networks.

Additional VMware network adapters were added to pfSense for HR, Finance, Guest, and Public networks. Each interface was assigned a static gateway IP address, then firewall rules were configured to control traffic between networks.

---

## Network Design

| VMnet | VLAN Name | Network | pfSense Gateway |
|---|---|---|---|
| VMnet1 | IT | 10.10.10.0/24 | 10.10.10.254 |
| VMnet2 | HR | 10.10.20.0/24 | 10.10.20.254 |
| VMnet3 | Finance | 10.10.30.0/24 | 10.10.30.254 |
| VMnet4 | Guest | 10.10.40.0/24 | 10.10.40.254 |
| VMnet5 | Public | 10.10.50.0/24 | 10.10.50.254 |
| VMnet8 | WAN | 192.168.88.0/24 | DHCP |

---

## Step 1 - Add Network Adapters to pfSense in VMware

Power off the pfSense VM before adding adapters.

Open:

```text
pfSense VM > Settings

Add the following network adapters:

Adapter	VMware Network	Purpose
Network Adapter 1	VMnet8	WAN / Internet
Network Adapter 2	VMnet1	IT / LAN
Network Adapter 3	VMnet2	HR
Network Adapter 4	VMnet3	Finance
Network Adapter 5	VMnet4	Guest
Network Adapter 6	VMnet5	Public

For each adapter, enable:

Connected
Connect at power on
Custom: Specific VMnet
Step 2 - Assign Interfaces in pfSense Console

Power on pfSense.

From the pfSense console menu, select:

1) Assign Interfaces

When asked:

Should VLANs be set up now?

Enter:

n

Assign interfaces as follows:

pfSense Interface	NIC	Network
WAN	em0	VMnet8
LAN	em1	VMnet1 / IT
OPT1	em2	VMnet2 / HR
OPT2	em3	VMnet3 / Finance
OPT3	em4	VMnet4 / Guest
OPT4	em5	VMnet5 / Public

When asked to proceed, enter:

y
Step 3 - Configure Interface IP Addresses from pfSense Console

From the pfSense console menu, select:

2) Set interface(s) IP address

Configure each interface using static IPv4 addresses.

Configure HR Interface

Select:

OPT1

Set:

IPv4 address: 10.10.20.254
Subnet bit count: 24
Upstream gateway: Press Enter for none
IPv6: n
DHCP server: n
HTTP webConfigurator: n
Configure Finance Interface

Select:

OPT2

Set:

IPv4 address: 10.10.30.254
Subnet bit count: 24
Upstream gateway: Press Enter for none
IPv6: n
DHCP server: n
HTTP webConfigurator: n
Configure Guest Interface

Select:

OPT3

Set:

IPv4 address: 10.10.40.254
Subnet bit count: 24
Upstream gateway: Press Enter for none
IPv6: n
DHCP server: n
HTTP webConfigurator: n
Configure Public Interface

Select:

OPT4

Set:

IPv4 address: 10.10.50.254
Subnet bit count: 24
Upstream gateway: Press Enter for none
IPv6: n
DHCP server: n
HTTP webConfigurator: n
Step 4 - Rename Interfaces in pfSense GUI

Open pfSense Web GUI:

https://10.10.10.254

Go to:

Interfaces

Rename interface descriptions:

Original Name	New Description
OPT1	HR
OPT2	Finance
OPT3	Guest
OPT4	Public

For each interface:

Enable interface
Description: HR / Finance / Guest / Public
IPv4 Configuration Type: Static IPv4

Verify IP addresses:

Interface	IPv4 Address
HR	10.10.20.254/24
Finance	10.10.30.254/24
Guest	10.10.40.254/24
Public	10.10.50.254/24

Click:

Save > Apply Changes
Step 5 - Update DHCP Scope Options on DC01

On DC01, open:

Server Manager > Tools > DHCP

For each scope, update:

Scope Options > 003 Router

Use the correct gateway for each network:

DHCP Scope	003 Router
IT	10.10.10.254
HR	10.10.20.254
Finance	10.10.30.254
Guest	10.10.40.254
Public	10.10.50.254

DNS option:

006 DNS Servers: 10.10.10.10
Step 6 - Firewall Rule Design

The final firewall design is:

Network	Access Policy
IT	Full access
HR	Access to IT and internet
Finance	Access to IT and internet
Guest	Internet only
Public	Reserved for future hosted services / DMZ
Step 7 - IT Firewall Rule

Go to:

Firewall > Rules > LAN

Keep the default allow rule:

Pass | LAN net | any

This allows IT administrators to access all networks.

Step 8 - HR Firewall Rule

Go to:

Firewall > Rules > HR

Add or keep:

Field	Value
Action	Pass
Interface	HR
Address Family	IPv4
Protocol	Any
Source	HR net
Destination	Any

Description:

Allow HR to IT and Internet

Click:

Save > Apply Changes
Step 9 - Finance Firewall Rule

Go to:

Firewall > Rules > Finance

Add or keep:

Field	Value
Action	Pass
Interface	Finance
Address Family	IPv4
Protocol	Any
Source	Finance net
Destination	Any

Description:

Allow Finance to IT and Internet

Click:

Save > Apply Changes
Step 10 - Guest Firewall Rules

Guest should access the internet only and should not access internal networks.

Go to:

Firewall > Rules > Guest

Create the following rules in order.

Guest Rule 1 - Block Guest to IT
Field	Value
Action	Block
Interface	Guest
Address Family	IPv4
Protocol	Any
Source	Guest net
Destination	LAN net

Description:

Block Guest to IT
Guest Rule 2 - Block Guest to HR
Field	Value
Action	Block
Interface	Guest
Address Family	IPv4
Protocol	Any
Source	Guest net
Destination	HR net

Description:

Block Guest to HR
Guest Rule 3 - Block Guest to Finance
Field	Value
Action	Block
Interface	Guest
Address Family	IPv4
Protocol	Any
Source	Guest net
Destination	Finance net

Description:

Block Guest to Finance
Guest Rule 4 - Allow Guest to Internet

Place this rule below the block rules.

Field	Value
Action	Pass
Interface	Guest
Address Family	IPv4
Protocol	Any
Source	Guest net
Destination	Any

Description:

Allow Guest Internet Access

Click:

Save > Apply Changes
Step 11 - Public Firewall Rule

For now, the Public network is reserved for future hosted services such as a web server or DMZ service.

Go to:

Firewall > Rules > Public

Add:

Field	Value
Action	Pass
Interface	Public
Address Family	IPv4
Protocol	Any
Source	Public net
Destination	Any

Description:

Allow Public Internet Access

This allows future public-facing servers to reach the internet for updates, DNS, certificate renewal, and package downloads.

Step 12 - Testing
Test HR Client

Connect a test client to:

VMnet2

Run:

ipconfig /release
ipconfig /renew
ipconfig /all

Expected:

IP Address: 10.10.20.x
Default Gateway: 10.10.20.254
DNS Server: 10.10.10.10

Test:

ping 10.10.20.254
ping 10.10.10.10
ping 8.8.8.8
Test Finance Client

Connect a test client to:

VMnet3

Expected:

IP Address: 10.10.30.x
Default Gateway: 10.10.30.254
DNS Server: 10.10.10.10

Test:

ping 10.10.30.254
ping 10.10.10.10
ping 8.8.8.8
Test Guest Client

Connect a test client to:

VMnet4

Expected:

IP Address: 10.10.40.x
Default Gateway: 10.10.40.254
DNS Server: 10.10.10.10

Guest should reach the internet:

ping 8.8.8.8

Guest should not reach internal networks:

ping 10.10.10.10
ping 10.10.20.254
ping 10.10.30.254

Expected result:

Internal network access blocked
Internet access allowed
Step 13 - Snapshot

After successful testing, create a VMware snapshot.

Snapshot name:

pfSense Inter-VLAN Routing and Firewall Rules Configured

Snapshot description:

pfSense configured with dedicated interfaces for IT, HR, Finance, Guest, and Public networks. Static gateway IPs assigned, DHCP scopes updated, and firewall rules configured. IT has full access, HR and Finance have access to IT and internet, Guest is restricted to internet only, and Public is reserved for future hosted services.
Key Concepts
VMware VMnets are used to simulate VLAN segmentation.
pfSense acts as the central router and firewall.
DC01 remains responsible for Active Directory, DNS, and DHCP.
RRAS is no longer used for routing.
Firewall rules are applied on the source interface where traffic enters pfSense.
Guest traffic is restricted using block rules above an allow-internet rule.
Final Architecture
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
