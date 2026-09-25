# Windows Server & Active Directory Lab

A hands-on enterprise infrastructure lab using **Proxmox, Windows Server, Active Directory Domain Services (AD DS), DNS, Group Policy, and Windows client systems**.

## 🎯 Project Overview

This project documents the design, deployment, configuration, and troubleshooting of a small Windows-based enterprise environment.

The objective is to develop practical skills in:

* Windows Server administration
* Active Directory Domain Services
* DNS and network configuration
* Domain authentication
* User and computer management
* Organizational Units (OUs)
* Group Policy
* Windows client administration
* Remote Desktop
* Network troubleshooting
* Virtualization using Proxmox

## 🏗️ Lab Architecture

The lab is being built using Proxmox virtualization.

```text
                    Proxmox
                       │
              ┌────────┴────────┐
              │                 │
           DC01              CLIENT01
       Windows Server        Windows 11
       Domain Controller       Client
              │                 │
              └───────┬─────────┘
                      │
                 lab.local
```

> The architecture diagram will be expanded as additional components are added to the lab.

## 🖥️ Current Environment

| Component         | Configuration    |
| ----------------- | ---------------- |
| Virtualization    | Proxmox VE       |
| Server            | Windows Server   |
| Domain Controller | DC01             |
| Domain            | `lab.local`      |
| DC01 IP           | `192.168.60.148` |
| Subnet            | `255.255.254.0`  |
| Gateway           | `192.168.60.1`   |
| DNS               | `8.8.8.8`        |

## 📋 Implementation Progress

* [x] Deploy Windows Server VM
* [x] Configure static IP address
* [x] Rename server to `DC01`
* [x] Install Active Directory Domain Services
* [x] Create `lab.local` forest
* [x] Promote DC01 to Domain Controller
* [x] Verify Domain Controller functionality
* [x] Create organizational unit structure
* [x] Create first domain user
* [ ] Test domain authentication
* [ ] Configure Windows client VM
* [ ] Join Windows client to the domain
* [ ] Configure Group Policy
* [ ] Configure and test RDP
* [ ] Configure shared resources and permissions
* [ ] Document troubleshooting scenarios
* [ ] Finalize architecture documentation

## 📂 Documentation

Detailed implementation notes are organized in the following sections:

* [Windows Server & Active Directory Setup](documentation/setup.md)
* Network Configuration
* Active Directory
* DNS
* Group Policy
* Windows Client Administration
* Remote Desktop
* Troubleshooting

Additional documentation will be added as the lab progresses.

## 🧪 Validation & Troubleshooting

The lab will include practical validation and troubleshooting exercises rather than configuration alone.

Examples will include:

* DNS resolution testing
* Domain connectivity testing
* Domain authentication
* Client domain membership
* Group Policy application
* Remote Desktop connectivity
* User and permission troubleshooting

## 🛠️ Technologies

* Proxmox VE
* Windows Server
* Windows 11
* Active Directory Domain Services
* DNS
* Group Policy
* Remote Desktop
* PowerShell
* Windows networking tools

## 📸 Screenshots

Screenshots documenting the implementation and validation of the lab will be added as the project progresses.

## 🎯 Project Goal

The goal of this lab is to develop and demonstrate practical skills in **Windows infrastructure, network administration, centralized identity management, and technical troubleshooting** through a documented hands-on environment.
