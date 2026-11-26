# DHCP Server – Verification and Testing

## 1. Objective

This section documents the verification of the DHCP server configuration and the network settings assigned to domain clients.

The goal is to confirm that DHCP01 correctly assigns IP addresses, provides the required network configuration and supports DNS name resolution within the `lab.local` domain.

## 2. DHCP Server Information

| Configuration | Value |
|---|---|
| DHCP Server | DHCP01 |
| FQDN | DHCP01.lab.local |
| IPv4 Address | 192.168.178.232 |
| Domain | lab.local |
| Network | 192.168.178.0/24 |

## 3. DHCP Scope Verification

The configured IPv4 scope was checked using:

```powershell
Get-DhcpServerv4Scope -ComputerName DHCP01
```

The following configuration was confirmed:

| Configuration | Verified Value |
|---|---|
| Scope ID | 192.168.178.0 |
| Subnet Mask | 255.255.255.0 |
| Start IP Address | 192.168.178.240 |
| End IP Address | 192.168.178.250 |
| Scope State | Active |
| Lease Duration | 8 hours |

The DHCP scope is active and ready to assign IP addresses to network clients.

## 4. DHCP Scope Options Verification

The scope options were checked using:

```powershell
Get-DhcpServerv4OptionValue -ComputerName DHCP01 -ScopeId 192.168.178.0
```

The following options were confirmed:

| Option | Description | Configured Value |
|---|---|---|
| 003 | Default Gateway | 192.168.178.1 |
| 006 | DNS Servers | 192.168.178.230, 192.168.178.231 |
| 015 | DNS Domain Name | lab.local |
| 051 | Lease Duration | 691200 seconds (8 hours) |

## 5. DHCP Lease Verification

The assigned IP addresses were checked using:

```powershell
Get-DhcpServerv4Lease -ComputerName DHCP01 -ScopeId 192.168.178.0 |
Format-Table HostName, IPAddress, AddressState, LeaseExpiryTime
```

The following active leases were found:

| Client | Assigned IPv4 Address | Lease State |
|---|---|---|
| CLIENT01.lab.local | 192.168.178.243 | Active |
| CLIENT02.lab.local | 192.168.178.240 | Active |

Both clients received addresses within the configured DHCP address pool.

## 6. Client Network Configuration Verification

The network configuration was checked directly on both Windows clients using:

```powershell
ipconfig /all
```

### CLIENT01

| Configuration | Verified Value |
|---|---|
| DHCP Enabled | Yes |
| IPv4 Address | 192.168.178.243 |
| Subnet Mask | 255.255.255.0 |
| DHCP Server | 192.168.178.232 |
| Default Gateway | 192.168.178.1 |
| DNS Servers | 192.168.178.230, 192.168.178.231 |
| DNS Suffix | lab.local |

### CLIENT02

| Configuration | Verified Value |
|---|---|
| DHCP Enabled | Yes |
| IPv4 Address | 192.168.178.240 |
| Subnet Mask | 255.255.255.0 |
| DHCP Server | 192.168.178.232 |
| Default Gateway | 192.168.178.1 |
| DNS Servers | 192.168.178.230, 192.168.178.231 |
| DNS Suffix | lab.local |

Both clients successfully received their network configuration from DHCP01.

## 7. DNS Resolution Verification

DNS name resolution was tested on CLIENT01 using:

```powershell
Resolve-DnsName DC01.lab.local
Resolve-DnsName DC02.lab.local
```

The following results were confirmed:

| DNS Name | Resolved IPv4 Address |
|---|---|
| DC01.lab.local | 192.168.178.230 |
| DC02.lab.local | 192.168.178.231 |

Both domain controllers were successfully resolved through DNS.

## 8. Domain Controller Connectivity

Network connectivity to both domain controllers was tested from CLIENT01 using:

```powershell
Test-Connection DC01.lab.local -Count 2
Test-Connection DC02.lab.local -Count 2
```

Both domain controllers responded successfully to two connection tests each.

This confirms network connectivity from CLIENT01 to DC01 and DC02.

## 9. Screenshots

The following screenshots document the verification process:

- DHCP scope overview showing the active state and address range
- DHCP scope options (Gateway, DNS Servers and DNS Domain Name)
- DHCP leases showing CLIENT01 and CLIENT02
- CLIENT01 network configuration (`ipconfig /all`)
- CLIENT02 network configuration (`ipconfig /all`)
- DNS resolution results for DC01 and DC02
- Connectivity test results using `Test-Connection`

<img width="974" height="624" alt="Screenshot 2026-11-21 204720" src="https://github.com/user-attachments/assets/d03a32e9-1291-4159-a629-d0e40e61b048" />
<img width="856" height="616" alt="Screenshot 2026-11-21 204531" src="https://github.com/user-attachments/assets/77c0e67f-88d2-44ad-a722-906a7f043e0b" />
<img width="805" height="644" alt="image" src="https://github.com/user-attachments/assets/428cf17b-646a-4ace-abf0-458c2cad05c9" />

## 10. Result

The DHCP configuration on DHCP01 was successfully verified.

The following results were confirmed:

- DHCP scope is active.
- The configured address pool is correct.
- DHCP scope options provide the correct gateway and DNS settings.
- Both domain clients received valid dynamic IP addresses.
- Both clients use DHCP01 as their DHCP server.
- Both clients received the correct DNS server addresses and domain suffix.
- DNS resolution for DC01 and DC02 succeeded on CLIENT01.
- Network connectivity from CLIENT01 to both domain controllers was successful.

The DHCP server is functioning correctly in the `lab.local` test environment.

**Note:** DNS resolution and connectivity tests were performed on CLIENT01. CLIENT02's DHCP configuration was verified separately.
