# DNS Forward and Reverse Lookup Zones

## 1. Objective

Document the DNS zones used in the `lab.local` Active Directory environment.

DNS supports both forward name resolution (hostname to IP address) and reverse name resolution (IP address to hostname).

## 2. Active Directory-Integrated DNS Zones

The following DNS zones are present in the lab environment:

| DNS Zone | Purpose |
|---|---|
| `lab.local` | Forward lookup of domain names |
| `_msdcs.lab.local` | Active Directory service records and Domain Controller discovery |
| `178.168.192.in-addr.arpa` | Reverse lookup of IPv4 addresses |

Active Directory-integrated DNS zones are stored in Active Directory and replicated between Domain Controllers.

Both DC01 and DC02 host these replicated DNS zones.

## 3. Reverse Lookup Zone

The reverse lookup zone for the lab network is:

```text
178.168.192.in-addr.arpa
```

A reverse lookup zone allows DNS to resolve IP addresses into hostnames using PTR records.

### Example Records

| IP Address | Hostname |
|---|---|
| `192.168.178.230` | `DC01.lab.local` |
| `192.168.178.231` | `DC02.lab.local` |

## 4. PTR Record Verification

The following commands were used to query the PTR records:

```powershell
Resolve-DnsName 192.168.178.230 -Type PTR
Resolve-DnsName 192.168.178.231 -Type PTR
```

The queries displayed the corresponding hostnames:

- `192.168.178.230` → `DC01.lab.local`
- `192.168.178.231` → `DC02.lab.local`

## 5. Hostnames and Fully Qualified Domain Names

When managing Domain Controllers, it is recommended to use DNS hostnames or Fully Qualified Domain Names (FQDN) whenever possible.

| Connection Type | Example |
|---|---|
| IP Address | `192.168.178.231` |
| Hostname | `DC02` |
| Fully Qualified Domain Name | `DC02.lab.local` |

Active Directory relies heavily on DNS for:

- Domain Controller discovery.
- Kerberos authentication.
- Active Directory replication.
- Service location through DNS SRV records.

Using an IP address is not always incorrect. However, some authentication mechanisms and services depend on correct hostname resolution.

## 6. Forward DNS Name Resolution

The following commands were used to query the hostnames:

```powershell
Resolve-DnsName DC01.lab.local
Resolve-DnsName DC02.lab.local
```

The observed results included:

| Hostname | Record Type | Resolved Address |
|---|---|---|
| `DC01.lab.local` | A | `192.168.178.230` |
| `DC02.lab.local` | A | `192.168.178.231` |
| `DC02.lab.local` | AAAA | `fe80::18df:7093:3178:1338` |

The AAAA record shown above is a link-local IPv6 address.

**Best Practice:** Verify DNS name resolution before troubleshooting Active Directory connectivity or replication issues.

## 7. Summary

The lab environment uses forward and reverse DNS zones to support name resolution.

The `lab.local` and `_msdcs.lab.local` zones provide internal domain name and service-record resolution. The reverse lookup zone supports IP address-to-hostname resolution.
