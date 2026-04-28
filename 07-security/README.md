## Security Configuration

### Multi-Factor Authentication (MFA)
- Enabled MFA for all users in Azure AD (Entra ID)
- Configured authentication methods (Microsoft Authenticator)
- Tested MFA login for user accounts

### Conditional Access Policies
- Created Conditional Access policies:
  - Require MFA for all users
  - Block legacy authentication
  - Restrict access based on location/device
- Verified policy enforcement during login

### Endpoint Security
- Configured Microsoft Defender policies
- Enabled real-time protection
- Applied security baselines for Windows devices

### Access Control
- Implemented least privilege access model
- Assigned roles based on user responsibilities
- Restricted administrative privileges

### Network Security
- Configured basic firewall rules in lab environment
- Secured communication between servers and clients
- Validated secure access to resources

### Monitoring & Validation
- Reviewed sign-in logs in Azure AD
- Monitored security alerts
- Verified policy application and compliance
