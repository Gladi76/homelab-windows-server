# DNS Forwarders and Root Hints on DC02

## 1. Objective

Document the DNS forwarding configuration on DC02 and explain how external DNS names can be resolved when no DNS forwarder is configured.

## 2. Previous DNS Forwarder Configuration

Initially, DC02 was configured to forward DNS queries to DC01 (`192.168.178.230`).

The forwarder was subsequently removed.

## 3. Current DNS Configuration

DC02 no longer has a configured DNS forwarder pointing to DC01.

The following command was used to check the configuration:

```powershell
Get-DnsServerForwarder
```

Observed configuration:

- No forwarder IP addresses configured.
- `UseRootHint` is set to `True`.

## 4. DNS Recursion

DNS recursion is enabled on DC02.

It was checked using:

```powershell
Get-DnsServerRecursion
```

Observed result:

```text
Enable : True
```

Recursion allows the DNS Server to resolve queries on behalf of clients by following the DNS resolution process.

## 5. Root Hints

Root Hints contain the addresses of public DNS root servers (A through M).

They provide starting points for resolving names through the public DNS hierarchy.

The configured Root Hints were checked using:

```powershell
Get-DnsServerRootHint
```

The command returned the configured root server entries.

## 6. How External DNS Resolution Works

When a client requests an external DNS name, such as `www.microsoft.com`, DC02 can use Root Hints to start the resolution process:

1. DC02 contacts a DNS root server.
2. The root server provides information about the responsible top-level domain servers, such as `.com`.
3. The `.com` DNS servers provide information about the authoritative DNS servers for the requested domain.
4. The authoritative DNS server provides the requested DNS record.
5. DC02 returns the result to the requesting client.

This process is called recursive DNS resolution.

## 7. Internal and External DNS

The internal Active Directory domain `lab.local` does not need to be publicly registered for external DNS resolution to work.

Internal DNS zones and public DNS resolution are separate functions.

Both DC01 and DC02 host the replicated Active Directory-integrated DNS zones. Removing the forwarder does not disable Active Directory DNS zone replication.

## 8. Summary

The current DNS configuration on DC02 has the following characteristics:

- No DNS forwarder configured.
- DNS recursion enabled.
- Root Hints enabled as the fallback mechanism.
- Active Directory-integrated DNS zones available locally.
