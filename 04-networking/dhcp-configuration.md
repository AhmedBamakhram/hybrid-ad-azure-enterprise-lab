# DHCP Configuration (Multi-VLAN)

## Overview

This section documents the configuration of DHCP on DC01 to provide automatic IP addressing for all VLAN networks.

Each VLAN has its own DHCP scope with a defined IP range, gateway, and DNS configuration.

---

## Install DHCP Role

1. Open **Server Manager**

2. Click:

```plaintext
Manage → Add Roles and Features
