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
```

Next - Next - Next

 Selecte **Role-based or feature-based installation**

 Next 

 Keep as its **Select destination server**

 Next
 
Select role:
✔ DHCP Server
 Add Features 
 Next - Next - Next - Install

 After " Feature installation " 
 Close

 On server Manager : 
 Click in falg with sclminattion mak 'Notifications'

 Click "Complete DHCP congfiguration"

 Click Next

 Choose :
 ✔ Use the following user's credentials
LAB\Administrator

Click Commit
Then Close
 
