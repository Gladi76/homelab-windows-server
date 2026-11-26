# Active Directory Domain Services (AD DS) and DNS Installation

## Overview

This section documents the installation of the Active Directory Domain Services (AD DS) and DNS Server roles on Windows Server 2022 (DC01).

These roles are required to establish and manage an Active Directory domain environment.

## Server Information

| Configuration | Value |
|---|---|
| Server Name | DC01 |
| Operating System | Windows Server 2022 Datacenter |
| Domain | lab.local |
| Server Role | Domain Controller |

## Installation Using PowerShell

The following PowerShell command was used to install the required server roles:

```powershell
Install-WindowsFeature AD-Domain-Services, DNS -IncludeManagementTools
```

### Installed Roles

| Server Role | Purpose |
|---|---|
| Active Directory Domain Services | Provides centralized authentication and directory services |
| DNS Server | Resolves domain names and supports Active Directory services |

## Verification

The installation was verified using PowerShell:

```powershell
Get-WindowsFeature AD-Domain-Services, DNS
```

### Verification Result

Both server roles are reported as installed:

- Active Directory Domain Services: Installed
- DNS Server: Installed

## Screenshot

<img width="794" height="207" alt="image" src="https://github.com/user-attachments/assets/feda8397-c31c-42d5-87a6-c484edf38047" />

## Status

Active Directory Domain Services and DNS Server roles are installed on DC01.
