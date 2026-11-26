# DHCP Server – Scope Configuration

## 1. Objective

This section documents the creation and configuration of an IPv4 DHCP scope on DHCP01.

The DHCP scope defines the range of IP addresses that can be dynamically assigned to clients in the `lab.local` network.

## 2. DHCP Server Information

| Configuration | Value |
|---|---|
| DHCP Server | DHCP01.lab.local |
| IPv4 Address | 192.168.178.232 |
| Active Directory Domain | lab.local |
| Network | 192.168.178.0/24 |

## 3. DHCP Scope Creation

A new IPv4 scope was created using the DHCP management console.

The following steps were performed:

1. Open **Server Manager → Tools → DHCP**.
2. Expand the DHCP server `DHCP01.lab.local`.
3. Right-click **IPv4**.
4. Select **New Scope**.
5. Enter a scope name and description.
6. Define the IP address range.
7. Configure the required scope options.
8. Complete the wizard.

## 4. DHCP Address Pool

The following address range was configured:

| Configuration | Value |
|---|---|
| Network Address | 192.168.178.0 |
| Subnet Mask | 255.255.255.0 |
| Start IP Address | 192.168.178.240 |
| End IP Address | 192.168.178.250 |
| Address Range | 192.168.178.240 – 192.168.178.250 |

The DHCP server dynamically assigns available IP addresses from this range to network clients.

## 5. DHCP Scope Options

The following DHCP scope options were configured:

| DHCP Option | Description | Configured Value |
|---|---|---|
| 003 | Router / Default Gateway | 192.168.178.1 |
| 006 | DNS Servers | 192.168.178.230, 192.168.178.231 |
| 015 | DNS Domain Name | lab.local |

### Explanation

- **Option 003 – Router:** Provides clients with the default gateway for communication outside their local network.
- **Option 006 – DNS Servers:** Provides DC01 and DC02 as DNS servers for domain name resolution.
- **Option 015 – DNS Domain Name:** Provides the DNS suffix `lab.local` to DHCP clients.

All three options were configured at the scope level and are displayed with the policy name `None`.

## 6. Scope Activation

After completing the scope configuration, the scope was activated.

An active scope allows DHCP01 to assign IP addresses to requesting clients.

## 7. Client Address Assignment

Two Windows clients successfully received dynamic IP addresses from DHCP01.

| Client | Assigned IPv4 Address | Assignment Type |
|---|---|---|
| CLIENT01.lab.local | 192.168.178.243 | DHCP |
| CLIENT02.lab.local | 192.168.178.240 | DHCP |

The assigned addresses are within the configured DHCP address pool.

## 8. Screenshots

The following screenshots document the DHCP scope configuration:

- DHCP IPv4 scope overview
- Configured address pool
- DHCP scope options (003, 006 and 015)
- DHCP address leases showing CLIENT01 and CLIENT02
<img width="826" height="510" alt="Screenshot 2026-11-20 231447" src="https://github.com/user-attachments/assets/0e656583-1ee1-467a-b41c-728e6da40d16" />
<img width="835" height="535" alt="Screenshot 2026-11-20 231749" src="https://github.com/user-attachments/assets/6877069a-7927-4d22-ab6c-a5c805696278" />
<img width="951" height="446" alt="Screenshot 2026-11-21 201317" src="https://github.com/user-attachments/assets/7f07ae79-f2f5-47a4-9798-320b18bae0cb" />
<img width="996" height="426" alt="Screenshot 2026-11-21 185245" src="https://github.com/user-attachments/assets/ff956ae5-34db-4091-a1dc-0932a78413b8" />

## 9. Result

The IPv4 DHCP scope was successfully configured and activated on DHCP01.

The address pool contains IP addresses from `192.168.178.240` to `192.168.178.250`.

The DHCP scope provides the default gateway, both domain DNS servers and the DNS domain name to requesting clients.

Both domain clients successfully received dynamic IP addresses from DHCP01.

The next step is to verify the DHCP configuration and client connectivity.
