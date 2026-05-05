# 14 - Install & Configure RRAS (Routing Between VLANs)

## Overview

In this step, Routing and Remote Access Service (RRAS) was installed and configured on DC01 to enable inter-VLAN routing between multiple network segments in the lab environment.

RRAS allows communication between isolated VLAN networks such as IT, HR, Finance, Guest, and Servers.

---

## Prerequisites

Before configuring RRAS, DC01 must have:

- Multiple network adapters, one per VLAN
- Each adapter connected to a separate VMware VMnet
- Static IP address configured on each adapter
- No default gateway configured on internal VLAN adapters

---

## VLAN Gateway Configuration

| VLAN | Network | DC01 Gateway IP |
|---|---|---|
| IT | 10.10.10.0/24 | 10.10.10.1 |
| HR | 10.10.20.0/24 | 10.10.20.1 |
| Finance | 10.10.30.0/24 | 10.10.30.1 |
| Guest | 10.10.40.0/24 | 10.10.40.1 |
| Servers | 10.10.50.0/24 | 10.10.50.1 |

> Note: Default gateway should be left blank on the internal VLAN interfaces.

---

## Step 1 - Install Remote Access Role

1. Open **Server Manager**
2. Click **Manage**
3. Select **Add Roles and Features**
4. Choose **Role-based or feature-based installation**
5. Select server **DC01**
6. Select the **Remote Access** role
7. Under **Role Services**, select:
   - **Routing**
8. Click **Next**
9. Click **Install**

---

## Step 2 - Open Routing and Remote Access

1. Open **Server Manager**
2. Click **Tools**
3. Select **Routing and Remote Access**

---

## Step 3 - Configure RRAS

1. Right-click **DC01 (local)**
2. Select **Configure and Enable Routing and Remote Access**
3. Click **Next**
4. Select **Custom configuration**
5. Click **Next**
6. Select **LAN routing**
7. Click **Next**
8. Click **Finish**

---

## Step 4 - Start RRAS Service

After completing the wizard:

1. Click **Start service**
2. Confirm that DC01 shows a green status icon in the RRAS console

---

## Step 5 - Verify RRAS Status

RRAS is successfully running when:

- DC01 shows a green arrow/status icon
- IPv4 routing options are visible
- The RRAS service is running

Optional command verification:

```cmd
sc query remoteaccess
