# 05 – Verification and Troubleshooting

## Overview

After installing Active Directory Domain Services (AD DS) and DNS, the configuration of DC01 was verified using Windows Server diagnostic tools and PowerShell.

## 1. Domain Controller Information

| Setting | Value |
|---|---|
| Server Name | DC01 |
| FQDN | DC01.lab.local |
| Domain | lab.local |
| Forest | lab.local |
| Operating System | Windows Server 2022 Datacenter |
| IP Address | 192.168.178.230 |
| Global Catalog | Enabled |
| Writable Domain Controller | Yes |

## 2. FSMO Roles

The following command was used to verify the FSMO roles:

```powershell
netdom query fsmo
```

All five FSMO roles are assigned to DC01.lab.local:

- Schema Master
- Domain Naming Master
- PDC Emulator
- RID Pool Manager
- Infrastructure Master

## 3. DNS Verification

DNS zones were checked using:

```powershell
Get-DnsServerZone
```

The following Active Directory-integrated zones are present:

- lab.local
- _msdcs.lab.local
- 178.168.192.in-addr.arpa

DNS diagnostics were performed with:

```powershell
dcdiag /test:dns /v
```

The DNS diagnostic tests completed successfully.

## 4. Active Directory Verification

The installed roles were checked using:

```powershell
Get-WindowsFeature AD-Domain-Services, DNS
```

Both roles are installed.

The domain controller configuration was checked using:

```powershell
Get-ADDomainController -Identity DC01
```

DC01 is recognized as an enabled, writable domain controller and Global Catalog.

## 5. Replication and Domain Diagnostics

The following commands were used:

```powershell
dcdiag /v
```

```powershell
dcdiag /test:replications
```

```powershell
repadmin /replsummary
```

The Active Directory replication test completed successfully.

DC01 is currently the only domain controller in the lab domain. Therefore, no active replication partners are expected at this stage.

## 6. SYSVOL and NETLOGON

The SYSVOL and NETLOGON shares were verified using:

```powershell
Get-SmbShare | Where-Object Name -in "SYSVOL","NETLOGON"
```

Both shares are available.

The DFS Replication service status was checked using:

```powershell
Get-Service DFSR
```

The service is running.

## 7. Current Status

- Windows Server 2022 Datacenter installed
- Active Directory Domain Services installed
- DNS Server installed and configured
- Domain `lab.local` created
- DC01 successfully promoted to a domain controller
- All five FSMO roles assigned to DC01
- DNS diagnostic tests successful
- Active Directory replication test successful
- SYSVOL and NETLOGON shares available
- DFS Replication service running

## Next Step

Prepare and configure DC02 as an additional domain controller in the existing `lab.local` domain.

