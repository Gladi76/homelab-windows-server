# DHCP Server – Active Directory Authorization

## 1. Objective

This section documents the authorization of DHCP01 in Active Directory.

In an Active Directory domain environment, a DHCP server must be authorized before it can provide DHCP services to domain clients.

## 2. Server Information

| Configuration | Value |
|---|---|
| Server Name | DHCP01 |
| FQDN | DHCP01.lab.local |
| IPv4 Address | 192.168.178.232 |
| Active Directory Domain | lab.local |
| DHCP Server Role | Installed |

## 3. DHCP Server Authorization

The DHCP server was authorized in Active Directory using the DHCP management console.

The following steps were performed:

1. Open **Server Manager**.
2. Select **Tools → DHCP**.
3. Open the DHCP management console.
4. Right-click the DHCP server `DHCP01.lab.local`.
5. Select **Authorize**.
6. Refresh the DHCP console.
7. Verify the authorization status.

The authorization registers DHCP01 as an approved DHCP server in Active Directory.

## 4. Authorization Verification

The authorization status was verified using PowerShell.

The command was executed using a domain administrator account:

```powershell
Get-DhcpServerInDC
```

Verified output:

```text
IPAddress            DnsName
---------            -------
192.168.178.232      dhcp01.lab.local
```

The output confirms that DHCP01 is registered as an authorized DHCP server in Active Directory.

## 5. Screenshots

The following screenshots document the authorization process:

- DHCP management console showing DHCP01
- PowerShell output of `Get-DhcpServerInDC`
<img width="783" height="448" alt="image" src="https://github.com/user-attachments/assets/d71e6746-421a-4696-91f0-5cc0d1080e0e" />
<img width="957" height="369" alt="image" src="https://github.com/user-attachments/assets/c702953e-f76f-4b86-89e0-bc044f3e92fe" />

## 6. Result

DHCP01 was successfully authorized in Active Directory and registered as an approved DHCP server for the domain `lab.local`.

The server is now ready for DHCP scope configuration.

The next step is to create the DHCP scope, define the address pool and configure the required scope options.
