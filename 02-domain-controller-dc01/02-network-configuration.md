# Network Configuration – DC01

## Overview

This section describes the network configuration of the Windows Server 2022 Domain Controller (DC01).

A static IPv4 address is configured to ensure reliable network communication and DNS services within the Active Directory environment.

## Network Configuration

| Configuration | Value |
|---|---|
| Computer Name | DC01 |
| Network Adapter | Ethernet |
| IP Address | 192.168.178.230 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.178.1 |
| Preferred DNS Server | 192.168.178.230 |
| Network Type | External Virtual Switch |

## Configuration Verification

The network configuration was checked using PowerShell:

```powershell
Get-NetIPConfiguration
```

DNS configuration was checked using:

```powershell
Get-DnsClientServerAddress -AddressFamily IPv4
```

## Screenshot

### Static IPv4 Configuration

The following screenshot shows the static IPv4 configuration of DC01.

<img width="944" height="602" alt="Screenshot 2026-11-19 000212" src="https://github.com/user-attachments/assets/9555e594-7f47-4d2f-baed-69c2e37de466" />


## Status

Static IPv4 configuration documented for DC01.
