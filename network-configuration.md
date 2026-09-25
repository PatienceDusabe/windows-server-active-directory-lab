# Network Configuration

## Windows Server — DC01

The Windows Server VM was configured with a static IPv4 address to provide a stable address for Active Directory and DNS services.

| Parameter       | Configuration    |
| --------------- | ---------------- |
| Hostname        | `DC01`           |
| IPv4 Address    | `192.168.60.148` |
| Subnet Mask     | `255.255.254.0`  |
| Default Gateway | `192.168.60.1`   |
| DNS             | `8.8.8.8`        |

## Purpose

A static IP address was assigned to the Domain Controller because domain services require a predictable network address.

The server will later provide Active Directory and DNS services to Windows client systems in the lab.

## Validation

Network connectivity was tested successfully after configuring the static IP settings.
