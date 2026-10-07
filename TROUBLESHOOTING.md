# Troubleshooting Guide

This document records common issues encountered while building and testing the Windows Server Active Directory lab.

## 1. Windows Server IP Address Changed

### Problem
The Windows Server IP address changed during the lab, which caused connectivity and domain communication problems.

### Resolution
The server was configured with a static IP address and the network configuration was verified using:

```powershell
ipconfig
```

Connectivity was then tested between the Domain Controller and Windows 11 client.

---

## 2. Windows 11 Could Not Initially Communicate Correctly With the Domain Controller

### Problem
The Windows 11 client experienced connectivity problems during the domain configuration process.

### Resolution
The IP configuration, gateway, DNS configuration, and connectivity between the client and Domain Controller were verified.

The client was eventually successfully joined to:

```text
lab.local
```

---

## 3. Domain Authentication

### Problem
There was confusion between the NetBIOS domain name and the full DNS domain name.

### Resolution
The Active Directory domain was confirmed as:

```text
lab.local
```

The NetBIOS name used for authentication was:

```text
LAB
```

Therefore, domain users can authenticate using:

```text
LAB\username
```

---

## 4. Group Policy Testing

### Problem
A desktop-background policy was difficult to validate because the Windows 11 installation was not activated.

### Resolution
The Group Policy configuration was verified using Group Policy tools instead of relying only on the visual desktop result.

The following commands were useful:

```powershell
Get-GPO -Name "Staff-Workstation-Policy"
```

and:

```powershell
Get-GPInheritance -Target "OU=Staff,DC=lab,DC=local"
```

---

## 5. Shared Folder Permissions

### Problem
The administrator account could access the private IT folder, making it initially difficult to determine whether the permissions were working correctly.

### Resolution
Testing was performed using the standard user account `user02`.

Expected behavior:

| Resource | IT-Users | IT-Admins |
|---|---|---|
| IT Public | Modify | Full Control |
| IT Private | Denied | Full Control |

The test confirmed that `user02` could create and edit files in `Public` but was denied access to `Private`.

---

## 6. RDP Connection Failed

### Problem
Remote Desktop initially appeared not to work.

### Troubleshooting

The following components were checked:

### Remote Desktop

Remote Desktop was confirmed to be enabled on DC01.

### Remote Desktop Service

```powershell
Get-Service TermService
```

The service was confirmed to be running.

### Firewall

```powershell
Get-NetFirewallRule -DisplayGroup "Remote Desktop" | Select DisplayName, Enabled
```

The relevant Remote Desktop firewall rules were enabled.

### RDP Port

```powershell
Get-NetTCPConnection -LocalPort 3389 -State Listen
```

DC01 was confirmed to be listening on TCP port `3389`.

### Client Connectivity

From Windows 11:

```powershell
Test-NetConnection DC01 -Port 3389
```

The result confirmed:

```text
TcpTestSucceeded : True
```

### RDP Security Policy

The Domain Controllers Group Policy was configured to allow:

```text
LAB\IT-Remote-Admins
```

under:

```text
Allow log on through Terminal Services
```

`Administrators` was also retained.

### Final Result

The Windows 11 client successfully established an RDP session with DC01 using the domain account:

```text
LAB\patience
```

The certificate warning displayed during the connection was expected in the lab environment because the remote computer's identity certificate was not trusted by the client.

---

## 7. General Troubleshooting Method

When troubleshooting an infrastructure problem, the following approach was used:

1. Verify the service.
2. Verify the configuration.
3. Verify firewall rules.
4. Verify network connectivity.
5. Verify authentication.
6. Verify authorization.
7. Test again after each change.

This approach prevents unnecessary configuration changes and helps identify the actual layer causing the problem.
