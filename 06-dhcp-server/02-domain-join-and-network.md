# DHCP Server – Domain Join and Network Configuration

## 1. Objective

This section documents the network configuration and domain integration of the dedicated DHCP server.

The server is configured with a static IPv4 address and joined to the existing Active Directory domain `lab.local`.

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
| IPv4 Address | 192.168.178.232 |
| Subnet Mask | 255.255.255.0 |
| Network | 192.168.178.0/24 |
| Preferred DNS Server | 192.168.178.230 (DC01) |
| Alternate DNS Server | 192.168.178.231 (DC02) |

Both domain controllers provide DNS services for the Active Directory domain.

Using DC01 and DC02 as DNS servers provides an alternative DNS server if one domain controller is temporarily unavailable.

## 4. Domain Join

DHCP01 was joined to the existing Active Directory domain:

`lab.local`

The domain join allows DHCP01 to authenticate within the domain and communicate with the domain controllers.

After joining the domain, the server was restarted to complete the process.

## 5. Verification

The following checks were performed to verify the configuration:

- Server hostname: `DHCP01`
- Static IPv4 address: `192.168.178.232`
- Preferred DNS server: `192.168.178.230`
- Alternate DNS server: `192.168.178.231`
- Domain membership: `lab.local`
- Server connectivity through Server Manager on DC01

## 6. Screenshots

Screenshots of the IPv4 configuration and domain membership will be added here.
<img width="787" height="505" alt="Screenshot 2026-11-20 224655" src="https://github.com/user-attachments/assets/e5f6c3b5-dc86-460c-92ef-918476628cbf" />
<img width="782" height="551" alt="Screenshot 2026-11-20 224819" src="https://github.com/user-attachments/assets/5a5f1866-40b0-4434-ab2d-3df09c023f59" />
<img width="785" height="556" alt="Screenshot 2026-11-20 224900" src="https://github.com/user-attachments/assets/e4b9cfe2-9bbe-48f7-a20c-4738dffbd6cd" />
<img width="780" height="553" alt="Screenshot 2026-11-20 225002" src="https://github.com/user-attachments/assets/9f91ee6d-9ce4-49b8-894f-3411f76453e5" />

## 7. Result

DHCP01 was configured with a static IPv4 address, both domain controllers as DNS servers, and successfully joined to the Active Directory domain `lab.local`.

The server is now prepared for installation of the DHCP Server role.

The next step is to install the DHCP Server role using Server Manager.
