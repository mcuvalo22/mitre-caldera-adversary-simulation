# Adversary Simulation with MITRE CALDERA

## Overview
This project was developed as part of the course  
**Information Systems Security (Sigurnost Informacijskih Sustava – SIS)**  
at the **Faculty of Organization and Informatics (FOI)**.

The goal of the project is to design and execute a simulated cyberattack
on a mock corporate network using **MITRE CALDERA**.
The project includes infrastructure design, adversary emulation,
deployment of defensive controls, and evaluation of detection effectiveness
based on the **MITRE ATT&CK framework**.

## Objectives
- Gain hands-on experience with adversary emulation and red/blue team workflows
- Design and secure a realistic enterprise network
- Execute CALDERA attack techniques mapped to MITRE ATT&CK
- Evaluate the effectiveness of security controls
- Develop technical documentation and incident analysis skills

## Project Deliverables
- Setup Guide (VM and network architecture, configuration)
- Attack–Defense Matrix (ATT&CK techniques vs detection)
- Incident Timeline with supporting evidence
- Final Security Report
- Demonstration of one attack and its detection/mitigation

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

## Technologies Used
- VirtualBox
- MITRE CALDERA
- Windows Active Directory
- Ubuntu Server
- MITRE ATT&CK Framework

## Documentation
Detailed setup instructions and analysis can be found in the `/docs` directory.

## Team
- **Mateo Čuvalo** – Infrastructure Engineer  
  Responsible for designing and configuring the virtualized enterprise network and core services.

- **Niko Ivančić** – Blue Team (Defense)  
  Focused on defensive strategies, monitoring, and detection of adversary activities.

- **Nikola Lazar** – Red Team (Adversary Simulation)  
  Responsible for executing attack scenarios and adversary simulations using MITRE CALDERA.

- **Roberto Šandro** – Threat Hunter Analyst  
  Analyzed attack behavior, identified indicators of compromise, and mapped findings to the MITRE ATT&CK framework.


## Disclaimer
This project is for **educational purposes only**.

