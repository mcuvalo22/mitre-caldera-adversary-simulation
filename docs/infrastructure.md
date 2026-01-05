# Infrastructure Design

This document describes the infrastructure used for the adversary simulation project.

## Network Configuration
- Network type: NAT Network (VirtualBox)
- Network name: CalderaNet
- Address range: 192.168.10.0/24
- DHCP: Enabled

The NAT Network allows all virtual machines to communicate with each other
while maintaining internet access and isolation from the host network.

## Virtual Machines Overview

### Domain Controller (DC)
- Operating System: Windows Server 2019/2022
- IP Address: 192.168.10.10 (static)
- Role: Active Directory Domain Services
- Domain name: corp.local

### Windows Workstation
- Operating System: Windows 10 Enterprise (Evaluation)
- Role: Domain-joined employee workstation
- DNS Server: 192.168.10.10

### Linux Server
- Operating System: Ubuntu Server
- Role: Internal Linux service host
- Services: SSH, Apache (optional)

### Attacker Machine
- Operating System: Kali Linux / Ubuntu
- Role: MITRE CALDERA server
