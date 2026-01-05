# Adversary Simulation with MITRE CALDERA

## Project Overview
This university project demonstrates adversary simulation using the **MITRE CALDERA** framework.
A mock enterprise network was designed and deployed in a virtualized environment to emulate real-world attack scenarios mapped to the **MITRE ATT&CK** framework.

## Academic Context
This project was developed as part of the course **Information Systems Security (Sigurnost Informacijskih Sustava – SIS)**  
at the **University of Zagreb, Faculty of Organization and Informatics (FOI)**.

The project aims to provide hands-on experience in adversary simulation,
enterprise network security, and attack technique mapping using the
MITRE ATT&CK framework.

## Infrastructure Overview
The simulated company network consists of:

- Windows Server (Domain Controller)
- Windows 10 Enterprise (Domain-joined workstation)
- Linux Server (Web / SSH service)
- Linux attacker machine running MITRE CALDERA

All machines are connected through an isolated **NAT Network** to ensure internal communication with internet access.

## Virtual Machines
| Machine | OS | Role |
|------|----|----|
| DC | Windows Server 2019/2022 | Active Directory Domain Controller |
| WS | Windows 10 Enterprise | Employee workstation |
| Linux | Ubuntu Server | Internal Linux server |
| Attacker | Kali Linux / Ubuntu | MITRE CALDERA server |

## Objectives
- Design a realistic enterprise network
- Deploy MITRE CALDERA
- Execute adversary simulations
- Map techniques to MITRE ATT&CK
- Analyze attack paths and results

## Technologies Used
- VirtualBox
- MITRE CALDERA
- Windows Active Directory
- Ubuntu Server
- MITRE ATT&CK Framework

## Documentation
Detailed setup instructions and analysis can be found in the `/docs` directory.

## Team
- Project members: Mateo Čuvalo, Niko Ivančić, Nikola Lazar, Roberto Šandro
- 
## Disclaimer
This project is for **educational purposes only**.

