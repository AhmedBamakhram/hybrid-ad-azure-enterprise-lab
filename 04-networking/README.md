## Networking Configuration

### IP Addressing
- Configured static IP address for Domain Controller (DC-01)
- Assigned IP ranges for internal network and DMZ
- Verified subnet configuration and gateway settings

### DNS Configuration
- Configured DNS on the Domain Controller
- Verified domain name resolution
- Tested client DNS lookup using nslookup

### DHCP Configuration
- Configured DHCP scope for client machines
- Assigned automatic IP addresses to domain clients
- Verified lease assignment and connectivity

### Network Segmentation
- Designed separate network zones:
  - Internal Network
  - DMZ Network
  - Management Network
  - VPN Network

### Connectivity Testing
- Tested ping between client and server
- Verified DNS resolution
- Confirmed domain join connectivity
- Tested remote access simulation through VPN

### Troubleshooting
- Checked IP configuration using ipconfig /all
- Tested DNS using nslookup
- Verified gateway and firewall rules
