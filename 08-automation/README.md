## Automation (PowerShell)

### User Management Automation
- Created users using PowerShell (New-ADUser)
- Automated bulk user creation using CSV import
- Assigned users to groups via scripts

### Group Management
- Created and managed security groups using PowerShell
- Automated group membership updates

### Azure Automation
- Used PowerShell to manage Azure AD users and roles
- Verified user synchronization and status

### System Administration Tasks
- Used PowerShell for:
  - Checking system information
  - Managing services
  - Running administrative commands

### Example Commands
```powershell
New-ADUser -Name "Test User" -GivenName "Test" -Surname "User" -SamAccountName "tuser" -UserPrincipalName "tuser@lab.local" -AccountPassword (ConvertTo-SecureString "Password123!" -AsPlainText -Force) -Enabled $true
