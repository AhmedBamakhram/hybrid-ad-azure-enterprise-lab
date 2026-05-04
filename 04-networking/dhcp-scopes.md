## Create DHCP Scopes

1. Open DHCP console:

```plaintext
dhcpmgmt.msc

Expand:
DC01
IPv4
Right-click:

IPv4 → New Scope
```
IT Scope
Scope Name: IT
IP Range:
Start: 10.10.10.100
End: 10.10.10.200
Subnet Mask: 255.255.255.0
Add Exclusions: (optional)
Lease Duration: Default
Configure Options
Default Gateway: 10.10.10.10
DNS Server: 10.10.10.10
Activate Scope: ✔ Yes
HR Scope
Scope Name: HR
IP Range:
Start: 10.10.20.100
End: 10.10.20.200
Subnet Mask: 255.255.255.0
Configure Options
Default Gateway: 10.10.20.1
DNS Server: 10.10.10.10
Activate Scope: ✔ Yes
Finance Scope
Scope Name: Finance
IP Range:
Start: 10.10.30.100
End: 10.10.30.200
Subnet Mask: 255.255.255.0
Configure Options
Default Gateway: 10.10.30.1
DNS Server: 10.10.10.10
Activate Scope: ✔ Yes
Guest Scope
Scope Name: Guest
IP Range:
Start: 10.10.40.100
End: 10.10.40.200
Subnet Mask: 255.255.255.0
Configure Options
Default Gateway: 10.10.40.1
DNS Server: 8.8.8.8
Activate Scope: ✔ Yes
Public Scope
Scope Name: Public
IP Range:
Start: 10.10.50.100
End: 10.10.50.200
Subnet Mask: 255.255.255.0
Configure Options
Default Gateway: 10.10.50.1
DNS Server: 8.8.8.8
Activate Scope: ✔ Yes
Notes
Each VLAN has its own DHCP scope
Gateway matches DC01 interface for each network
Internal VLANs use DC01 as DNS (10.10.10.10)
Guest/Public use external DNS for isolation
Scopes must be activated to start assigning IP addresses
Outcome
All VLANs receive IP addresses automatically
Clients can connect without manual configuration
Network is ready for routing and security configuration
---

# 🚀 Commit message

```plaintext
Add DHCP scopes configuration for multi-VLAN environment
```
