# DHCP Relay Configuration

## Overview

Because the DHCP server (DC01) is located on the IT subnet (`10.10.10.0/24`), devices located on different VLANs/subnets cannot directly receive DHCP broadcasts.

Routers and firewalls do not forward DHCP broadcast traffic by default.

To allow clients on HR, Finance, Guest, and Public networks to obtain IP addresses, DHCP Relay was configured on pfSense.

---

# Why DHCP Relay Was Required

| VLAN | Subnet | DHCP Server Reachable Without Relay |
|---|---|---|
| IT | 10.10.10.0/24 | Yes |
| HR | 10.10.20.0/24 | No |
| Finance | 10.10.30.0/24 | No |
| Guest | 10.10.40.0/24 | No |
| Public | 10.10.50.0/24 | No |

The DHCP server:

```text
DC01 = 10.10.10.10
```

was located only on the IT subnet.

---

# DHCP Relay Configuration Steps

## Open pfSense Web Interface

```text
https://10.10.10.254
```

---

## Navigate to DHCP Relay

```text
Services → DHCP Relay
```

---

## Enable DHCP Relay

Enable:

```text
Enable DHCP Relay
```

---

## Configure Interfaces

Selected Interfaces:

- HR
- Finance
- Guest
- Public

The IT/LAN interface was excluded because the DHCP server already resides on that subnet.

---

## Configure Upstream DHCP Server

Upstream DHCP Server:

```text
10.10.10.10
```

---

## Save Configuration

1. Click:
   - Save
2. Click:
   - Apply Changes

---

# DHCP Renewal on Client Machines

After enabling DHCP Relay, DHCP leases were renewed on client systems.

Commands used:

```cmd
ipconfig /release
ipconfig /renew
```

---

# Result

Client systems successfully obtained IP addresses from the centralized DHCP server across multiple VLANs/subnets.

| Client | Assigned Network |
|---|---|
| IT-PC01 | 10.10.10.0/24 |
| HR-PC01 | 10.10.20.0/24 |
| FIN-PC01 | 10.10.30.0/24 |
| GUEST-PC01 | 10.10.40.0/24 |

---

# Enterprise Concept

This configuration simulates a real-world enterprise network design where:

- DHCP services are centralized
- Multiple VLANs/subnets exist
- Routers/firewalls use DHCP Relay (IP Helper) to forward DHCP requests
- Network segmentation is enforced using pfSense
