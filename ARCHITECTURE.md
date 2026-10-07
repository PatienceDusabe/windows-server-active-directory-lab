# Lab Infrastructure Architecture

## Overview

This project is a small enterprise-style Windows infrastructure laboratory built using Proxmox virtualization.

The purpose of the lab is to practice:

- Virtualization
- Windows Server administration
- Active Directory
- Domain authentication
- Organizational Units
- Group Policy
- User and group management
- File sharing and permissions
- Remote Desktop Services
- Network troubleshooting
- Infrastructure documentation

---

## High-Level Architecture

```text
                         Home / Lab Network
                                |
                                |
                         +------+------+
                         |   Proxmox   |
                         |    Host     |
                         +------+------+
                                |
              +-----------------+-----------------+
              |                                   |
              |                                   |
       +------+-------+                     +-----+------+
       |    DC01      |                     | Windows 11 |
       | Windows      |                     |   Client   |
       |   Server     |                     |            |
       +------+-------+                     +-----+------+
              |                                   |
              |                                   |
              +----------- Domain -----------------+
                          lab.local
```

---

## Main Components

### Proxmox Host

The Proxmox server provides the virtualization platform for the laboratory.

It hosts the virtual machines used for the infrastructure exercises.

---

## DC01

### Operating System

Windows Server

### Hostname

```text
DC01
```

### Domain

```text
lab.local
```

### Main Responsibilities

DC01 provides the core Windows infrastructure services for the lab:

- Active Directory Domain Services
- Domain authentication
- Organizational Units
- User accounts
- Security groups
- Group Policy
- File sharing
- NTFS permissions
- Remote Desktop access

DC01 acts as the Domain Controller for the `lab.local` domain.

---

## Windows 11 Client

The Windows 11 virtual machine represents an employee workstation.

It is joined to:

```text
lab.local
```

The client is used to test:

- Domain authentication
- Group Policy
- File access
- User permissions
- Remote Desktop
- Network connectivity

The domain user `patience` was successfully used to authenticate against the domain.

---

## Active Directory Structure

The following Organizational Units were created:

```text
lab.local
|
+-- Computers
|
+-- IT
|
+-- Management
|
+-- Staff
|
+-- Users
```

The structure provides a foundation for applying different policies and permissions to different categories of users and computers.

---

## Security Groups

The IT Organizational Unit contains role-based security groups:

```text
IT
|
+-- IT-Admins
|
+-- IT-Users
|
+-- IT-Remote-Admins
```

### IT-Admins

Used for users requiring administrative access to IT resources.

### IT-Users

Used for normal IT users requiring access to shared IT resources.

### IT-Remote-Admins

Used specifically to control which users are permitted to connect to DC01 using Remote Desktop.

This follows a role-based access approach instead of assigning permissions individually to each user.

---

## Group Policy

Two policies were created for the Staff environment:

```text
Staff-Workstation-Policy
Staff-Security-Policy
```

### Staff-Workstation-Policy

Contains workstation-related configuration.

### Staff-Security-Policy

Contains security-related configuration, including:

- User Account Control behavior
- Removable storage restrictions

Group Policy inheritance was verified on the Staff OU.

---

## File Sharing Architecture

Shared resources are located on DC01:

```text
C:\CompanyShares
|
+-- IT
    |
    +-- Public
    |
    +-- Private
```

The IT share is published as:

```text
\\DC01\IT
```

### Public

IT-Users have Modify access.

IT-Admins have Full Control.

### Private

IT-Admins have Full Control.

IT-Users do not have access.

This demonstrates the difference between shared resources and role-based permissions.

---

## Remote Desktop Architecture

Remote Desktop is enabled on DC01.

The access flow is:

```text
Windows 11 Client
       |
       | RDP / TCP 3389
       |
       v
      DC01
       |
       v
IT-Remote-Admins
       |
       v
    patience
```

The Windows 11 client successfully connected to DC01 using:

```text
LAB\patience
```

The RDP service was verified as running and TCP port `3389` was confirmed to be listening.

---

## Security Model

The lab follows a basic role-based security model:

```text
User
 |
 +--> Security Group
        |
        +--> Resource / Policy
```

Examples:

```text
user02
   |
   +--> IT-Users
          |
          +--> IT Public

patience
   |
   +--> IT-Admins
   |
   +--> IT-Remote-Admins
          |
          +--> Remote Desktop
```

This approach makes permissions easier to manage as the environment grows.

---

## Future Expansion

The architecture can later be expanded with additional infrastructure such as:

- Additional Windows clients
- File servers
- Backup infrastructure
- Monitoring
- DNS/DHCP services
- Printer management
- Security systems integration
- Linux servers
- Network services
- Centralized logging
- Automation

Additional servers should only be introduced when there is a clear requirement for a separate service or role.
