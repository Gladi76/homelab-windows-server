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

The PowerShell output for DC01 returned the A record in the `Answer` section.

For DC02, the expected A and AAAA records were displayed, but PowerShell showed them in the `Question` section.

## 4. Verify Reverse DNS Resolution

The following commands were used to query the reverse lookup records:

```powershell
Resolve-DnsName 192.168.178.230 -Type PTR
Resolve-DnsName 192.168.178.231 -Type PTR
```

Observed results:

- `192.168.178.230` → `DC01.lab.local`
- `192.168.178.231` → `DC02.lab.local`

The DC01 PTR record was returned in the `Answer` section.

The initial DC02 query returned `DC02.lab.local`, but the result was displayed in the `Question` section.

## 5. Direct DNS Query Against DC02

To further verify the DNS records of DC02, direct queries were sent to the DNS Server running on DC02.

### Reverse Lookup

```powershell
Resolve-DnsName 231.178.168.192.in-addr.arpa -Type PTR -Server 192.168.178.231
```

Observed result:

```text
Name                           Type   TTL   Section    NameHost
----                           ----   ---   -------    --------
231.178.168.192.in-addr.arpa   PTR    1200  Answer     DC02.lab.local
```

The PTR record was returned in the `Answer` section.

This confirms that the DNS Server on DC02 correctly resolves its own reverse DNS record.

### Forward Lookup

```powershell
Resolve-DnsName DC02.lab.local -Server 192.168.178.231
```

The expected A record was returned:

```text
DC02.lab.local → 192.168.178.231
```

An AAAA record for the link-local IPv6 address was also returned:

```text
fe80::18df:7093:3178:1338
```

The PowerShell output displayed these records in the `Question` section.

The expected DNS records were nevertheless returned by the direct query against DC02.

## 6. Verify External DNS Resolution

External DNS resolution was tested directly through DC02:

```powershell
Resolve-DnsName www.microsoft.com -Server 192.168.178.231 -DnsOnly
```

The query completed successfully.

The response included a CNAME chain:

```text
www.microsoft.com
        ↓
www.microsoft.com-c-3.edgekey.net
        ↓
e13678.dscb.akamaiedge.net
```

An IPv6 address was also returned:

```text
2a02:26f0:3380:ca3::356e
```

The result confirms that DC02 can successfully resolve external DNS names.

The successful external lookup is consistent with the configured Root Hints fallback.

However, the exact upstream DNS resolution path was not independently verified.

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
| DC01 forward DNS lookup | Successful |
| DC02 forward DNS lookup | Expected records returned |
| DC01 reverse DNS lookup | Successful |
| DC02 reverse DNS lookup | Successful – direct query returned `Answer` |
| External DNS lookup through DC02 | Successful |
| DNS recursion | Enabled |
| DNS forwarders | No forwarder configured |
| Root Hints | Configured |
| TCP connectivity to root server | Successful |
| Direct DNS query to root server | Unsuccessful |

## 9. Screenshot

The following screenshot shows the DNS verification tests performed on DC02.

<img width="983" height="488" alt="DNS verification on DC02" src="https://github.com/user-attachments/assets/a97d1f61-9f1e-402f-a677-015228e7e2da" />
<img width="975" height="496" alt="Direct DNS verification against DC02" src="https://github.com/user-attachments/assets/80d407cf-5889-4c8b-aa88-8ede8edddd49" />

## 10. Conclusion

The DNS Server on DC02 successfully resolves internal DNS records and external DNS names.

The reverse DNS record for DC02 was directly verified against the DNS Server running on DC02 and returned the expected `PTR` record in the `Answer` section.

The external DNS test through DC02 was also successful and returned a valid CNAME chain and IPv6 address.

DNS recursion is enabled and Root Hints are configured. No DNS forwarder to DC01 is currently configured.

The verification confirms that DC02 provides functional DNS services for both the internal Active Directory environment and external DNS resolution.
