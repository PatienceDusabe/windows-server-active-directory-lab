# Windows Server & Active Directory Setup

This document describes the deployment and configuration of the Windows Server and Active Directory environment used in this lab.

The environment was built on **Proxmox VE** and consists of a Windows Server Domain Controller and a Windows 11 client joined to the domain.

---

## 1. Lab Environment

### Infrastructure

| Component | Configuration |
|-----------|---------------|
| Hypervisor | Proxmox VE |
| Server VM | Windows Server |
| Server hostname | `DC01` |
| Domain | `lab.local` |
| Client VM | Windows 11 |
| Network | `192.168.60.0/23` |
| Gateway | `192.168.60.1` |
| DC01 IP | `192.168.61.253` |
| Subnet Mask | `255.255.254.0` |

The Windows Server VM was configured as the Domain Controller for the `lab.local` domain.

---

# 2. Deploy Windows Server VM

A Windows Server virtual machine was created in Proxmox.

The VM was configured with the resources required for the lab and Windows Server was installed from the Windows Server installation media.

After installation, the server was prepared for the infrastructure configuration.

---

# 3. Configure the Server Network

The server was configured with a static IPv4 address.

### DC01 network configuration

```text
IP Address:      192.168.61.253
Subnet Mask:     255.255.254.0
Default Gateway: 192.168.60.1
```

The server's network configuration was verified using Command Prompt.

```cmd
ipconfig
```

Additional connectivity testing was performed using:

```cmd
ping 192.168.60.1
```

The gateway was reachable from the server.

---

# 4. Rename the Server

The Windows Server computer was renamed to:

```text
DC01
```

The computer was restarted after the hostname change.

The hostname was verified from Command Prompt:

```cmd
hostname
```

Expected result:

```text
DC01
```

---

# 5. Install Active Directory Domain Services

The **Active Directory Domain Services (AD DS)** server role was installed using Server Manager.

The installation process was:

1. Open **Server Manager**.
2. Select **Add Roles and Features**.
3. Select **Role-based or feature-based installation**.
4. Select the local server.
5. Select **Active Directory Domain Services**.
6. Add the required management tools.
7. Complete the installation.

After installation, Server Manager displayed the notification indicating that the server needed to be promoted to a Domain Controller.

---

# 6. Create the Active Directory Forest

The server was promoted to a Domain Controller.

A new forest was created using:

```text
lab.local
```

The server became the first Domain Controller in the new forest.

### Domain

```text
lab.local
```

### Domain Controller

```text
DC01
```

The Domain Controller installation was completed and the server restarted.

---

# 7. Verify Active Directory

After the restart, the server was checked to confirm that it was operating as a Domain Controller.

The following administrative tools were used:

- Server Manager
- Active Directory Users and Computers
- DNS Manager
- Active Directory Domains and Trusts

The domain was confirmed as:

```text
lab.local
```

The Domain Controller was confirmed as:

```text
DC01
```

---

# 8. Active Directory Organizational Units

Organizational Units were created to provide a structured way of managing users and computers.

The following OUs were created:

```text
Computers
IT
Users
Management
Staff
```

The resulting structure provides separate administrative areas for different types of users and computers.

Example:

```text
lab.local
│
├── Computers
├── IT
├── Management
├── Staff
└── Users
```

---

# 9. Create Domain Users

A domain user was created for testing domain authentication.

The user account was created in Active Directory Users and Computers.

The account was then used to test authentication from the Windows 11 client.

The domain account was successfully used after the client was joined to:

```text
lab.local
```

---

# 10. Create Security Groups

Security groups were used to demonstrate centralized permission and administration management.

Groups were created in Active Directory and users could be assigned to the appropriate groups according to their administrative requirements.

This was also used during testing of permissions and administrative access.

---

# 11. Configure the Windows 11 Client

A Windows 11 client VM was deployed in Proxmox.

The client was configured to communicate with the Windows Server environment.

The client was tested for network connectivity before attempting to join the domain.

Basic connectivity was tested using:

```cmd
ping 192.168.61.253
```

The client was able to communicate with the Domain Controller.

---

# 12. Join Windows 11 to the Domain

The Windows 11 client was joined to the Active Directory domain:

```text
lab.local
```

The domain join process required domain credentials.

After the domain join completed, Windows 11 was restarted.

The client was then able to authenticate using a domain account.

---

# 13. Verify Domain Authentication

After joining the client to the domain, domain authentication was tested.

The Windows 11 client was used to sign in with the domain user.

The successful login confirmed that:

- The client was a member of `lab.local`.
- The Domain Controller was reachable.
- Active Directory authentication was functioning.
- The domain user account was valid.

The logged-in user and domain information could also be checked from Command Prompt.

```cmd
whoami
```

The computer's domain membership could be checked using:

```cmd
systeminfo
```

Network configuration could be checked using:

```cmd
ipconfig /all
```

---

# 14. Group Policy

Group Policy was configured to demonstrate centralized management of Windows users and computers.

The existing Organizational Units were used as the structure for applying policies.

Group Policy Management was accessed from the Domain Controller.

Policies were created and linked to the appropriate Organizational Units.

The Windows client was then used to verify that the policies were being applied.

A policy refresh could be triggered from Command Prompt:

```cmd
gpupdate /force
```

The resulting policies could be inspected using:

```cmd
gpresult /r
```

This provided practical experience with centralized Windows configuration management.

---

# 15. Security Policy Testing

The lab was also used to test Windows security controls.

One of the practical tests involved attempting to install software from the Windows client.

The installation was denied because of the configured security restrictions.

This demonstrated how centralized policies can prevent users from performing actions that are not permitted by the organization's security configuration.

The test was useful for validating that the configured security controls were actually being enforced on the client rather than simply existing in the Group Policy configuration.

---

# 16. Remote Desktop

Remote Desktop was configured and tested as part of the remote administration portion of the lab.

The server was configured to permit Remote Desktop connections.

The Windows client was then used to establish an RDP connection to the remote computer.

The connection was successfully established.

During testing, a warning concerning the identity of the remote computer was encountered.

The warning was investigated and the RDP connection was successfully completed.

This provided practical experience with:

- Remote Desktop configuration
- Remote authentication
- Domain credentials
- Remote computer identity warnings
- Windows remote administration

---

# 17. Command-Line Validation

Command Prompt and PowerShell were used throughout the lab for validation and troubleshooting.

Important commands used included:

### Check IP configuration

```cmd
ipconfig
```

### Detailed network configuration

```cmd
ipconfig /all
```

### Test network connectivity

```cmd
ping <IP-address>
```

Example:

```cmd
ping 192.168.61.253
```

### Check the current hostname

```cmd
hostname
```

### Check the logged-in account

```cmd
whoami
```

### Force Group Policy update

```cmd
gpupdate /force
```

### Display applied Group Policies

```cmd
gpresult /r
```

These commands were useful for validating the environment without relying exclusively on graphical administration tools.

---

# 18. Troubleshooting Experience

Several issues were encountered during the implementation of the lab.

The troubleshooting process was an important part of the project because the objective was not simply to configure the environment, but to understand how to identify and resolve infrastructure problems.

Troubleshooting areas included:

- Windows Server network configuration
- IP address changes and verification
- Client/server connectivity
- Domain connectivity
- Domain authentication
- Windows client domain joining
- Active Directory account authentication
- Group Policy application
- User permissions
- Software installation restrictions
- Remote Desktop connectivity
- Remote computer identity warnings

Problems were investigated using a combination of:

- Windows administrative tools
- Command Prompt
- PowerShell
- Network connectivity tests
- Active Directory Users and Computers
- Group Policy Management
- Server Manager

---

# 19. Validation Checklist

The completed environment was validated using the following tests.

| Test | Status |
|------|--------|
| Windows Server deployed | ✅ |
| Static IP configured | ✅ |
| Server renamed to DC01 | ✅ |
| AD DS installed | ✅ |
| `lab.local` forest created | ✅ |
| DC01 promoted to Domain Controller | ✅ |
| Domain Controller verified | ✅ |
| DNS configured | ✅ |
| Organizational Units created | ✅ |
| Domain users created | ✅ |
| Security groups configured | ✅ |
| Windows 11 client deployed | ✅ |
| Windows 11 joined to domain | ✅ |
| Domain authentication tested | ✅ |
| Group Policy configured | ✅ |
| Group Policy application tested | ✅ |
| Security restrictions tested | ✅ |
| Software installation restriction tested | ✅ |
| RDP configured | ✅ |
| RDP connection successfully tested | ✅ |
| Troubleshooting scenarios documented | ✅ |

---

# 20. Final Lab Architecture

The completed core environment can be represented as:

```text
                         Proxmox VE
                              │
                 ┌────────────┴────────────┐
                 │                         │
                 │                         │
              DC01                     CLIENT01
        Windows Server               Windows 11
        Domain Controller               Client
                 │                         │
                 │                         │
                 └───────────┬─────────────┘
                             │
                         lab.local
                             │
              ┌──────────────┼──────────────┐
              │              │              │
           Users             OUs         Group Policy
              │              │              │
              └──────────────┴──────────────┘
```

---

# 21. Skills Demonstrated

This lab demonstrates practical experience with:

### Windows Infrastructure

- Windows Server deployment
- Windows 11 administration
- Server configuration
- Network configuration
- Remote administration

### Active Directory

- AD DS installation
- Domain Controller deployment
- Forest creation
- Domain management
- User management
- Security groups
- Organizational Units
- Domain authentication

### Group Policy

- Group Policy configuration
- Policy assignment
- Policy application
- Client-side validation
- Security restriction testing

### Networking

- IPv4 configuration
- Subnet configuration
- Gateway configuration
- DNS configuration
- Connectivity testing
- Client/server communication

### Security

- Centralized authentication
- User permissions
- Security groups
- Group Policy enforcement
- Software installation restrictions
- Remote access control

### Troubleshooting

- Network troubleshooting
- Domain troubleshooting
- Authentication troubleshooting
- Group Policy troubleshooting
- Permission troubleshooting
- RDP troubleshooting
- Command-line diagnostics

---

# 22. Conclusion

This lab provides a practical demonstration of how a small enterprise Windows infrastructure can be deployed and administered using virtualization, Windows Server, Active Directory, DNS, Group Policy, and Windows client systems.

The project goes beyond installation by including **authentication testing, security policy validation, remote administration, command-line diagnostics, and troubleshooting**.

The environment provides a foundation for further infrastructure exercises, including additional Windows administration, file services, printer management, security systems integration, monitoring, and network services.
