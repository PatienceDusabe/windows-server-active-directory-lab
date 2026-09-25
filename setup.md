# Windows Server & Active Directory Setup

## 1. Virtual Machine Deployment

A Windows Server virtual machine was created in Proxmox VE.

The VM was configured as the primary server for the lab environment.

## 2. Network Configuration

The server was assigned a static IPv4 address:

`192.168.60.148/23`

The default gateway was configured as:

`192.168.60.1`

## 3. Server Naming

The server hostname was changed to:

`DC01`

The hostname reflects the server's intended role as the Domain Controller.

## 4. Active Directory Domain Services

The Active Directory Domain Services role was installed through Server Manager.

The server was then promoted to a new forest.

### Domain

`lab.local`

### Domain Controller

`DC01`

## 5. Organizational Units

A parent organizational unit named `LAB` was created with the following child OUs:

* Users
* Computers
* IT
* Management
* Staff

This structure will later be used to organize users and computers and apply Group Policy.

## 6. Domain User

A test domain user was created:

`LAB\patience`

The account will be used to test domain authentication and Group Policy behavior.

## Current Status

The Domain Controller is operational and `DC01` appears under the Domain Controllers container in Active Directory Users and Computers.

Further testing and client integration will be documented as the lab progresses.
