## Troubleshooting Scenarios

### Scenario 1: User Unable to Login
**Issue:**
User could not log into domain

**Troubleshooting Steps:**
- Checked user account status in Active Directory
- Verified account was not locked or disabled
- Reset user password

**Resolution:**
User successfully logged in after password reset

---

### Scenario 2: Group Policy Not Applying
**Issue:**
GPO settings not applied to client machine

**Troubleshooting Steps:**
- Ran gpupdate /force
- Checked OU placement
- Verified GPO linkage and permissions

**Resolution:**
Policy applied successfully after correcting OU placement

---

### Scenario 3: DNS Resolution Issue
**Issue:**
Client unable to resolve domain name

**Troubleshooting Steps:**
- Checked DNS configuration
- Verified client DNS points to Domain Controller
- Tested using nslookup

**Resolution:**
DNS fixed after correcting server configuration

---

### Scenario 4: Azure AD Sync Failure
**Issue:**
Users not syncing to Azure AD

**Troubleshooting Steps:**
- Checked Azure AD Connect service
- Verified synchronization status
- Forced manual sync

**Resolution:**
Users successfully synced to Azure

---

### Scenario 5: Device Not Compliant in Intune
**Issue:**
Device marked as non-compliant

**Troubleshooting Steps:**
- Checked compliance policies
- Verified device settings
- Re-synced device

**Resolution:**
Device became compliant after policy update

---

### Scenario 6: VPN Connectivity Issue
**Issue:**
Remote user unable to connect via VPN

**Troubleshooting Steps:**
- Checked network connectivity
- Verified credentials
- Tested VPN configuration

**Resolution:**
VPN access restored after configuration fix
