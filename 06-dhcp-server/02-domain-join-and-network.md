# DHCP Server – Domain Join and Network Configuration

## 1. Objective

This section documents the network configuration and domain integration of the dedicated DHCP server.

DHCP01 is configured with a static IPv4 address and joined to the existing Active Directory domain `lab.local`.

## 2. Server Identification

| Configuration | Value |
|---|---|
| Computer Name | DHCP01 |
| Fully Qualified Domain Name | DHCP01.lab.local |
| Active Directory Domain | lab.local |
| Server Role | DHCP Server |

## 3. Network Configuration

A static IPv4 configuration was assigned to DHCP01 to ensure that the server remains reachable at a predictable network address.

| Configuration | Value |
|---|---|
| Network Adapter | Ethernet |
| IPv4 Address | 192.168.178.232 |
| Subnet Mask | 255.255.255.0 |
| Network | 192.168.178.0/24 |
| Default Gateway | 192.168.178.1 |
| Preferred DNS Server | 192.168.178.230 (DC01) |
| Alternate DNS Server | 192.168.178.231 (DC02) |

Both domain controllers provide DNS services for the Active Directory domain.

## 4. Domain Join

DHCP01 was successfully joined to the existing Active Directory domain:

`lab.local`

After joining the domain, the server was restarted to complete the process.

## 5. Configuration Verification

The configuration was verified using PowerShell.

### 5.1 Domain Membership

Command:

```powershell
Get-CimInstance Win32_ComputerSystem |
Select-Object Name, Domain, PartOfDomain
```

Result:

```text
Name    Domain    PartOfDomain
----    ------    ------------
DHCP01  lab.local True
```

The output confirms that DHCP01 is a member of the `lab.local` domain.

### 5.2 Network Configuration

Command:

```powershell
Get-NetIPConfiguration
```

Verified configuration:

- Network adapter: Ethernet
- IPv4 address: 192.168.178.232
- Default gateway: 192.168.178.1
- Preferred DNS server: 192.168.178.230
- Alternate DNS server: 192.168.178.231

The network configuration matches the planned lab network.

### 5.3 Domain Secure Channel Verification

The secure channel between DHCP01 and the Active Directory domain can be checked using:

```powershell
Test-ComputerSecureChannel -Verbose
```

Expected result:

```text
True
```

A result of `True` confirms that the secure channel between DHCP01 and the domain is working correctly.

## 6. Screenshots

The following screenshots document the configuration and verification:

- Domain membership verification
- IPv4 network configuration
- DNS server configuration
- Domain secure channel verification
 <img width="959" height="512" alt="image" src="https://github.com/user-attachments/assets/d3c95bec-627f-4a1f-8c57-bc5e002f5129" />
 
## 7. Result

DHCP01 was successfully configured with a static IPv4 address and joined to the Active Directory domain `lab.local`.

The PowerShell verification confirmed the computer name, domain membership, IPv4 address, default gateway and both DNS server addresses.

The secure channel verification provides an additional check of the domain relationship.

The server is now prepared for installation of the DHCP Server role.
