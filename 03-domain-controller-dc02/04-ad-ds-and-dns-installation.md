# DC02 – Install AD DS and DNS Roles

## 1. Objective

Install the Active Directory Domain Services (AD DS) and DNS Server roles on DC02.

These roles are required to promote DC02 as an additional Domain Controller in the existing Active Directory domain `lab.local`.

## 2. Install Active Directory Domain Services

The AD DS role was installed using PowerShell:

```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```

The installation completed successfully.

## 3. Install DNS Server

The DNS Server role was installed using:

```powershell
Install-WindowsFeature DNS -IncludeManagementTools
```

The installation completed successfully.

## 4. Verify Installed Roles

The installed roles were checked using:

```powershell
Get-WindowsFeature AD-Domain-Services, DNS
```

Both roles were successfully installed.

## 5. Result

DC02 now has the following server roles installed:

- Active Directory Domain Services (AD DS)
- DNS Server

The server is prepared for promotion as an additional Domain Controller in the existing domain `lab.local`.

## 6. Screenshot

<img width="1205" height="622" alt="Screenshot 2026-11-20 002157" src="https://github.com/user-attachments/assets/823c67b6-5145-4429-9b45-bd8290c9a411" />


## Technischer Hinweis – Active Directory-Standorte (Sites)

In einer produktiven IT-Umgebung sollten zusätzliche Domänencontroller, die sich an unterschiedlichen physischen Netzwerkstandorten befinden, den entsprechenden Active Directory-Standorten (Sites) zugeordnet werden.

Active Directory Sites ermöglichen:

- Die Optimierung der Active Directory-Replikation zwischen verschiedenen Standorten.
- Die Steuerung des Authentifizierungsverkehrs.
- Die standortbezogene Ermittlung von Domänencontrollern über DNS.
- Die Reduzierung des Netzwerkverkehrs zwischen verschiedenen Standorten.

**Wichtig:** Ein zusätzlicher Domänencontroller benötigt nicht zwingend einen eigenen Active Directory-Standort. Domänencontroller am gleichen physischen Standort und im gleichen Netzwerk können derselben Site zugeordnet werden.

In dieser Homelab-Umgebung befinden sich DC01 und DC02 innerhalb derselben Active Directory-Site `Main-Site`.
