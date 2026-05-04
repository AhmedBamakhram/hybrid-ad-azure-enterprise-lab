# DHCP Scope Configuration for Multi-VLAN Environment

This document describes the creation and configuration of DHCP scopes on **DC01** for a segmented, VLAN-based network. Each VLAN has its own IP range, default gateway, and DNS configuration.

---

## 1. Open the DHCP Management Console

```plaintext
dhcpmgmt.msc
```

In the DHCP console:

```plaintext
DC01
└── IPv4
      └── Right-click → New Scope
```

---

## 2. Create DHCP Scopes

### 2.1 IT Scope

**Scope Name:** IT  
**IP Range:**
- Start: `10.10.10.100`
- End: `10.10.10.200`

**Subnet Mask:** `255.255.255.0`  
**Gateway:** `10.10.10.10`  
**DNS Server:** `10.10.10.10`  
**Activate:** Yes

**Steps:**

1. Right-click **IPv4** → **New Scope**.
2. Name the scope: `IT`.
3. Set IP range:
   - Start: `10.10.10.100`
   - End: `10.10.10.200`
   - Subnet mask: `255.255.255.0`
4. Add exclusions (optional), then click **Next**.
5. Keep lease duration as default, click **Next**.
6. Choose **Yes, I want to configure these options now**.
7. Configure **Router (Default Gateway)**: `10.10.10.10`, click **Next**.
8. Keep Domain Name and DNS server as `10.10.10.10`, click **Next**.
9. Skip WINS (click **Next**).
10. Select **Yes, I want to activate this scope now**, then click **Finish**.

---

### 2.2 HR Scope

**Scope Name:** HR  
**IP Range:**
- Start: `10.10.20.100`
- End: `10.10.20.200`

**Subnet Mask:** `255.255.255.0`  
**Gateway:** `10.10.20.1`  
**DNS Server:** `10.10.10.10`  
**Activate:** Yes

---

### 2.3 Finance Scope

**Scope Name:** Finance  
**IP Range:**
- Start: `10.10.30.100`
- End: `10.10.30.200`

**Subnet Mask:** `255.255.255.0`  
**Gateway:** `10.10.30.1`  
**DNS Server:** `10.10.10.10`  
**Activate:** Yes

---

### 2.4 Guest Scope

**Scope Name:** Guest  
**IP Range:**
- Start: `10.10.40.100`
- End: `10.10.40.200`

**Subnet Mask:** `255.255.255.0`  
**Gateway:** `10.10.40.1`  
**DNS Server:** `8.8.8.8`  
**Activate:** Yes

---

### 2.5 Public Scope

**Scope Name:** Public  
**IP Range:**
- Start: `10.10.50.100`
- End: `10.10.50.200`

**Subnet Mask:** `255.255.255.0`  
**Gateway:** `10.10.50.1`  
**DNS Server:** `8.8.8.8`  
**Activate:** Yes

---

## 3. Notes

- Each VLAN has its own DHCP scope.
- Gateways match the interface for each network on **DC01** or the router.
- Internal VLANs (IT, HR, Finance) use internal DNS: `10.10.10.10`.
- Guest and Public VLANs use external DNS for isolation.
- Scopes must be activated to start assigning IP addresses.

---

## 4. Outcome

- All VLANs receive IP addresses automatically.
- Clients connect without manual IP configuration.
- Network is ready for routing and security configuration.

---

## 5. Updating Scope Options

To update any scope configuration later (e.g., DNS, gateway):

```plaintext
Right-click Scope → Properties
```

To update scope options such as DNS:

```plaintext
Right-click Scope Options → Configure Options
```

---

## 6. Commit Message

```plaintext
Add DHCP scope configurations for multi-VLAN network environment
```
