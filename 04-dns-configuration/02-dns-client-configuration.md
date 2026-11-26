# DNS Client Configuration on DC02

## 1. Objective

Configure the DNS client settings on DC02 so that the server can resolve names in the existing Active Directory domain `lab.local`.

## 2. Configure DNS Server Address

The DNS client settings were configured using the Windows Server Configuration tool (SConfig).

### Configuration Steps

1. Open SConfig.
2. Select option `8` – Network Settings.
3. Select network interface index `1`.
4. Select option `2` – Set DNS Servers.
5. Enter the IP address of the preferred DNS server.

Initially, DC02 was configured to use DC01 (`192.168.178.230`) as its DNS server.

## 3. Verify DNS Client Configuration

The following PowerShell command displays the configured DNS server addresses:

```powershell
Get-DnsClientServerAddress -AddressFamily IPv4
```

## 4. Important Difference

The DNS client configuration and the DNS Server role are two different settings.

- **DNS client setting:** Determines which DNS server DC02 queries to resolve names.
- **DNS Server role:** Allows DC02 to provide DNS services to other clients.

## 5. Result

DC02 was configured to use DC01 as its DNS server for name resolution during the initial setup.
