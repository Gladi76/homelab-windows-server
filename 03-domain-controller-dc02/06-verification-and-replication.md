# DC02 – Verification and Replication

## 1. Objective

Verify the successful configuration of DC02 as an additional Domain Controller in the existing Active Directory domain `lab.local`.

The verification includes Domain Controller services, SYSVOL and NETLOGON shares, DNS configuration, and Active Directory replication.

## 2. Verify Domain Controllers

The available Domain Controllers were listed using:

```powershell
Get-ADDomainController -Filter * |
    Format-Table HostName, IPv4Address, Site, IsGlobalCatalog
```

Verified Domain Controllers:

| Domain Controller | IP Address | Site | Global Catalog |
|---|---|---|---|
| DC01.lab.local | 192.168.178.230 | Leipzig | True |
| DC02.lab.local | 192.168.178.231 | Leipzig | True |

## 3. Verify Domain Controller Services

The required services were checked on DC02:

```powershell
Get-Service NTDS, DNS, DFSR, Netlogon |
    Format-Table Name, Status, StartType
```

All four services were running:

- NTDS – Active Directory Domain Services
- DNS – DNS Server
- DFSR – DFS Replication
- Netlogon – Netlogon Service

## 4. Verify SYSVOL and NETLOGON Shares

The required network shares were checked using:

```powershell
Get-SmbShare |
    Where-Object Name -in "SYSVOL","NETLOGON"
```

Both shares were present:

- SYSVOL
- NETLOGON

These shares are required for Group Policy distribution and logon scripts.

## 5. Verify Active Directory Replication

The replication summary was checked using:

```powershell
repadmin /replsummary
```

**Result:**

- DC01: 0 replication errors
- DC02: 0 replication errors
- 0% replication failures

Detailed inbound replication was checked using:

```powershell
repadmin /showrepl
```

All five naming contexts were successfully replicated from DC01 to DC02:

- Domain
- Configuration
- Schema
- ForestDnsZones
- DomainDnsZones

The replication diagnostics were also executed:

```powershell
dcdiag /test:replications /v
```

**Result:** DC02 successfully passed the Replications test.

## 6. Verify DNS Zones

The DNS zones on DC02 were listed using:

```powershell
Get-DnsServerZone |
    Format-Table ZoneName, ZoneType, IsDsIntegrated
```

The following Active Directory-integrated zones were present:

- lab.local
- _msdcs.lab.local
- 178.168.192.in-addr.arpa

## 7. Verify DNS Name Resolution

DNS name resolution was tested using:

```powershell
Resolve-DnsName DC01.lab.local
Resolve-DnsName DC02.lab.local
```

Verified IPv4 addresses:

| Hostname | IPv4 Address |
|---|---|
| DC01.lab.local | 192.168.178.230 |
| DC02.lab.local | 192.168.178.231 |

Both Domain Controllers were successfully resolved through DNS.

## 8. Result

DC02 was successfully deployed as an additional writable Domain Controller in the existing Active Directory domain.

The following components were verified:

- Active Directory Domain Services
- DNS Server
- Global Catalog
- NTDS, DNS, DFSR and Netlogon services
- SYSVOL and NETLOGON shares
- Active Directory replication
- Active Directory-integrated DNS zones
- DNS name resolution

The replication summary reported zero errors on both Domain Controllers.

**Note:** The SYSVOL and NETLOGON shares were confirmed to exist. A separate SYSVOL replication diagnostic is required to verify full DFSR synchronization.
