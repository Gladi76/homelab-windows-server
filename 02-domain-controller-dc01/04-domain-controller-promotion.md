# Domain Controller Promotion – DC01

## Overview

This section documents the promotion of Windows Server 2022 (DC01) to an Active Directory Domain Controller.

DC01 was configured as the first Domain Controller in a new Active Directory forest.

## Domain Configuration

| Configuration | Value |
|---|---|
| Server Name | DC01 |
| Fully Qualified Domain Name | DC01.lab.local |
| Active Directory Domain | lab.local |
| Forest Name | lab.local |
| Domain Functional Level | To be verified |
| Forest Functional Level | To be verified |
| Global Catalog | Enabled |
| DNS Server | Installed |

## Promotion Process

The Active Directory Domain Services Configuration Wizard was used to promote DC01.

The following configuration was selected:

1. Selected **Add a new forest**.
2. Entered the root domain name: `lab.local`.
3. Selected the appropriate Domain Controller options.
4. Configured the Directory Services Restore Mode (DSRM) password.
5. Completed the prerequisite checks.
6. Started the promotion process.
7. Restarted the server after promotion.

## Verification

The Domain Controller configuration was verified using PowerShell:

```powershell
Get-ADDomainController -Identity DC01
```

The output confirmed:

- Domain: `lab.local`
- Host Name: `DC01.lab.local`
- Enabled: `True`
- Global Catalog: `True`
- Read-Write Domain Controller: `True`

## FSMO Roles

The FSMO role assignment was checked using:

```powershell
netdom query fsmo
```

All five FSMO roles are currently assigned to DC01.

## Screenshots

<img width="951" height="326" alt="image" src="https://github.com/user-attachments/assets/2265fb61-84a5-4bb6-891b-0f03e75a92de" />
<img width="661" height="287" alt="image" src="https://github.com/user-attachments/assets/1a3edc3b-88a5-4ede-b566-9b3c82bb435c" />

## Status

DC01 successfully promoted as the first Domain Controller in the `lab.local` Active Directory forest.
