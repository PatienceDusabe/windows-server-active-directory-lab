# Windows Server & Active Directory Lab

A hands-on enterprise infrastructure lab using **Proxmox, Windows Server, Active Directory Domain Services (AD DS), DNS, Group Policy, Remote Desktop, and Windows client systems**.

## 🎯 Project Overview

This project documents the design, deployment, configuration, testing, and troubleshooting of a small Windows-based enterprise environment.

The objective is to develop practical skills in:

- Windows Server administration
- Active Directory Domain Services
- DNS and network configuration
- Domain authentication
- User and computer management
- Organizational Units (OUs)
- Group Policy
- Windows client administration
- Remote Desktop
- Network troubleshooting
- Virtualization using Proxmox
- Windows security and access control

## 🏗️ Lab Architecture

The lab is deployed using Proxmox virtualization.

```text
                         Proxmox
                            │
              ┌─────────────┴─────────────┐
              │                           │
            DC01                       CLIENT01
       Windows Server                 Windows 11
      Domain Controller                 Client
              │                           │
              └─────────────┬─────────────┘
                            │
                       lab.local
```

The environment simulates a small enterprise Windows infrastructure with centralized identity management, client administration, security policies, and remote administration.

## 🖥️ Current Environment

| Component | Configuration |
|-----------|---------------|
| Virtualization | Proxmox VE |
| Server | Windows Server |
| Domain Controller | DC01 |
| Domain | `lab.local` |
| Windows Client | Windows 11 |
| DC01 IP | `192.168.61.253` |
| Subnet | `255.255.254.0` |
| Gateway | `192.168.60.1` |
| DNS | `8.8.8.8` |

## 📋 Implementation Progress

### Windows Server & Active Directory

- [x] Deploy Windows Server VM
- [x] Configure static IP address
- [x] Rename server to `DC01`
- [x] Install Active Directory Domain Services
- [x] Create `lab.local` forest
- [x] Promote DC01 to Domain Controller
- [x] Verify Domain Controller functionality
- [x] Configure DNS
- [x] Create organizational unit structure
- [x] Create domain users
- [x] Configure security groups
- [x] Test domain authentication

### Windows 11 Client

- [x] Deploy Windows 11 client VM
- [x] Configure network connectivity
- [x] Configure DNS for domain connectivity
- [x] Join Windows 11 client to `lab.local`
- [x] Create and use a domain user
- [x] Test domain authentication from the client
- [x] Verify communication between client and Domain Controller

### Group Policy & Security

- [x] Create and organize domain OUs
- [x] Configure Group Policy
- [x] Apply policies to domain users/computers
- [x] Test policy application
- [x] Test Windows security restrictions
- [x] Validate software installation restrictions

### Remote Administration

- [x] Configure Remote Desktop
- [x] Test RDP connectivity
- [x] Authenticate through the domain
- [x] Troubleshoot remote computer identity/certificate warnings
- [x] Successfully establish an RDP session

### Shared Resources & Permissions

- [x] Configure shared resources
- [x] Test user access and permissions
- [x] Test access using domain accounts
- [x] Troubleshoot access and permissions

### Validation & Troubleshooting

- [x] Test network connectivity
- [x] Test DNS resolution
- [x] Test domain connectivity
- [x] Test domain authentication
- [x] Test client domain membership
- [x] Test Group Policy application
- [x] Test Remote Desktop connectivity
- [x] Test user permissions
- [x] Document troubleshooting scenarios
- [ ] Finalize architecture documentation
- [ ] Finalize screenshot documentation

## 📂 Documentation

Detailed implementation notes are organized in the following sections:

- [Windows Server & Active Directory Setup](documentation/setup.md)
- Network Configuration
- Active Directory
- DNS
- Group Policy
- Windows Client Administration
- Remote Desktop
- Security & Access Control
- Troubleshooting

Additional documentation and screenshots will be added as the lab is finalized.

## 🧪 Validation & Troubleshooting

This project focuses on **practical validation and troubleshooting**, rather than configuration alone.

The environment has been used to test:

- Network connectivity
- DNS resolution
- Domain communication
- Domain authentication
- Windows client domain membership
- Organizational Unit structure
- Group Policy application
- User and computer permissions
- Software installation restrictions
- Remote Desktop connectivity
- Remote authentication
- Windows security behavior
- Remote computer identity/certificate warnings

Troubleshooting was performed using both the Windows graphical administration tools and command-line utilities such as **Command Prompt and PowerShell**.

## 🔐 Security & Access Control

The lab also demonstrates basic enterprise security concepts, including:

- Centralized user authentication
- Domain-based access control
- Security group membership
- Organizational Unit-based administration
- Group Policy enforcement
- Software installation restrictions
- User permissions
- Remote Desktop access control

These exercises demonstrate how Windows administrators can centrally manage users, computers, and security policies within a domain environment.

## 🛠️ Technologies

- Proxmox VE
- Windows Server
- Windows 11
- Active Directory Domain Services
- DNS
- Group Policy
- Remote Desktop Protocol (RDP)
- PowerShell
- Command Prompt
- Windows networking tools

## 📸 Screenshots

Screenshots are being added to document key stages of deployment, configuration, validation, and troubleshooting.

Planned screenshot categories include:

- Windows Server configuration
- Active Directory Domain Services
- Domain and OU structure
- Domain users and groups
- Windows 11 domain membership
- Group Policy configuration
- Group Policy validation
- Security policy testing
- RDP configuration and successful connection
- Command-line validation and troubleshooting

## 🎯 Project Goal

The goal of this lab is to develop and demonstrate practical skills in **Windows infrastructure, network administration, centralized identity management, security administration, remote administration, and technical troubleshooting** through a documented hands-on enterprise environment.

The project demonstrates not only the ability to deploy Windows infrastructure, but also the ability to **configure, test, troubleshoot, secure, and document** the resulting environment.
