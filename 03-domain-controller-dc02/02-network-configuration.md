# DC02 – Network Configuration

## 1. Objective

Configure a static IPv4 address for DC02 to ensure reliable network communication with DC01 and the existing Active Directory domain.

## 2. Network Configuration

DC02 uses the same external Hyper-V virtual switch as DC01.

The following static network configuration was applied:

| Setting | Value |
|---|---|
| Computer Name | DC02 |
| Network Adapter | Ethernet |
| IP Address | 192.168.178.231 |
| Subnet Mask | 255.255.255.0 |
| Prefix Length | 24 |
| Default Gateway | 192.168.178.1 |
| Preferred DNS Server | 192.168.178.230 |
| DNS Server Hostname | DC01.lab.local |

## 3. Configure the Static IP Address

The network adapter was identified using PowerShell:

```powershell
Get-NetAdapter
```

The static IPv4 configuration was applied with the following commands:

```powershell
New-NetIPAddress `
    -InterfaceIndex 3 `
    -IPAddress "192.168.178.231" `
    -PrefixLength 24 `
    -DefaultGateway "192.168.178.1"
```

The DNS server was configured to use DC01:

```powershell
Set-DnsClientServerAddress `
    -InterfaceIndex 3 `
    -ServerAddresses "192.168.178.230"
```

## 4. Verify Network Configuration

The network configuration was checked using:

```powershell
Get-NetIPConfiguration
```

The DNS configuration was checked using:

```powershell
Get-DnsClientServerAddress -AddressFamily IPv4
```

## 5. Result

DC02 was successfully configured with a static IPv4 address.

The server uses DC01 as its preferred DNS server to locate the existing Active Directory domain.

Network configuration:

- DC01: 192.168.178.230
- DC02: 192.168.178.231
- Default Gateway: 192.168.178.1
- DNS Server: 192.168.178.230
