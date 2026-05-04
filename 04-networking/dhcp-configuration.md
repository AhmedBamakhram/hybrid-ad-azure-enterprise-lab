# DHCP Configuration (Multi-VLAN)

## Overview

This section documents the configuration of DHCP on DC01 to provide automatic IP addressing for all VLAN networks.

Each VLAN has its own DHCP scope with a defined IP range, gateway, and DNS configuration.

---

## Install DHCP Role

1. Open **Server Manager**

2. Click:
   **Manage → Add Roles and Features**

3. In the wizard:

- Click **Next**
- Select:
  - ✔ **Role-based or feature-based installation**
- Click **Next**

4. Server Selection:

- Keep default:
  - ✔ **Select destination server (DC01)**
- Click **Next**

5. Server Roles:

- Select:
  - ✔ **DHCP Server**
- Click **Add Features**
- Click **Next**

6. Continue:

- Click **Next → Next → Next**
- Click **Install**

---

## Complete Installation

- After the feature installation completes, click **Close**

---

## Post-Install DHCP Configuration

1. In **Server Manager**, click the **notification flag (⚠️)**

2. Click:
   **Complete DHCP configuration**

3. Click **Next**

4. Authorization:

- Select:
  - ✔ **Use the following user's credentials**
  - `LAB\Administrator`

5. Click **Commit**

6. Click **Close**
