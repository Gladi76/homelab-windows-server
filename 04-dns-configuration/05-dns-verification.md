# DNS Verification on DC02

## 1. Objective

Verify internal and external DNS name resolution through the DNS Server running on DC02.

## 2. Verify DNS Client Configuration

The DNS client configuration was checked using:

```powershell
Get-DnsClientServerAddress -AddressFamily IPv4
```

This command displays the DNS servers configured on the network interface.

## 3. Verify Internal DNS Resolution

The following commands were used to test the resolution of the Domain Controllers:

```powershell
Resolve-DnsName DC01.lab.local
Resolve-DnsName DC02.lab.local
```

Observed results:

| Hostname | Record Type | Resolved Address |
|---|---|---|
| `DC01.lab.local` | A | `192.168.178.230` |
| `DC02.lab.local` | A | `192.168.178.231` |
| `DC02.lab.local` | AAAA | `fe80::18df:7093:3178:1338` |

The AAAA record shown above is a link-local IPv6 address.

The PowerShell output for DC01 returned the A record in the `Answer` section. The DC02 records were displayed in the `Question` section.

## 4. Verify Reverse DNS Resolution

The following commands were used to query the reverse lookup records:

```powershell
Resolve-DnsName 192.168.178.230 -Type PTR
Resolve-DnsName 192.168.178.231 -Type PTR
```

The observed results were:

- `192.168.178.230` → `DC01.lab.local`
- `192.168.178.231` → `DC02.lab.local`

The DC01 PTR record was returned in the `Answer` section.

The DC02 PTR query returned `DC02.lab.local`, but the PowerShell output displayed the result in the `Question` section.

## 5. Direct DNS Query Against DC02

To further verify the DC02 DNS records, direct queries against the DNS Server running on DC02 were performed.

### Reverse Lookup

```powershell
Resolve-DnsName 231.178.168.192.in-addr.arpa -Type PTR -Server 192.168.178.231
```

### Forward Lookup

```powershell
Resolve-DnsName DC02.lab.local -Server 192.168.178.231
```

These tests query the DNS service on DC02 directly instead of relying on the DNS client configuration.

The results are used to verify whether DC02 can directly provide its own forward and reverse DNS records.

## 6. Verify External DNS Resolution

External DNS resolution was tested directly through DC02:

```powershell
Resolve-DnsName www.microsoft.com -Server 192.168.178.231 -DnsOnly
```

The query completed successfully and returned:

- CNAME records pointing to Microsoft's content delivery network.
- IPv4 address: `23.37.194.81`
- Multiple IPv6 address records.

This confirms that DC02 successfully resolved an external DNS name.

The successful result is consistent with the configured Root Hints fallback. However, the exact upstream DNS path was not independently verified.

## 7. Additional Root Server Diagnostic Test

A TCP connectivity test was performed against an IPv4 DNS root server:

```powershell
Test-NetConnection 198.41.0.4 -Port 53
```

The TCP connection succeeded.

However, direct DNS queries to this root server using `Resolve-DnsName` were unsuccessful during testing.

**Note:** A successful TCP connection to port 53 does not prove that DNS queries over UDP are working. The successful external DNS lookup through DC02 is a separate test.

## 8. Final Verification Summary

| Test | Result |
|---|---|
| Internal forward DNS lookup | Records returned |
| DC01 reverse DNS lookup | Successful |
| DC02 reverse DNS lookup | Hostname returned; direct verification performed |
| External DNS lookup through DC02 | Successful |
| DNS recursion | Enabled |
| DNS forwarders | No forwarder configured |
| Root Hints | Configured |
| TCP connectivity to root server | Successful |
| Direct DNS query to root server | Unsuccessful |

## 9. Screenshot

The following screenshot shows the DNS resolution tests performed on DC02.

<img width="983" height="488" alt="DNS verification on DC02" src="https://github.com/user-attachments/assets/a97d1f61-9f1e-402f-a677-015228e7e2da" />
<img width="975" height="496" alt="image" src="https://github.com/user-attachments/assets/80d407cf-5889-4c8b-aa88-8ede8edddd49" />


## 10. Conclusion

The DNS Server on DC02 successfully resolves internal hostnames and external DNS names.

The internal Active Directory DNS zones are available on both Domain Controllers through Active Directory integration and replication.

DNS recursion is enabled and Root Hints are configured. The external DNS resolution test through DC02 was successful.

The direct DNS queries against DC02 provide an additional verification step for the forward and reverse DNS records of DC02.
