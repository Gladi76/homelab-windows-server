# DC02 – Join the Active Directory Domain

## 1. Objective

Join the Windows Server 2022 machine DC02 to the existing Active Directory domain `lab.local`.

DC01 is the existing Domain Controller and provides Active Directory and DNS services.

## 2. Verify Domain Controller Connectivity

Before joining the domain, DC02 was checked to ensure that it could locate DC01.

```powershell
nltest /dsgetdc:lab.local
```

The command successfully discovered:

- Domain Controller: DC01.lab.local
- IP Address: 192.168.178.230
- Site: Main-Site

## 3. Join the Domain

The following PowerShell command was executed on DC02:

```powershell
Add-Computer -DomainName "lab.local" -Credential (Get-Credential) -Restart
```

The domain administrator credentials were provided when prompted.

The server restarted automatically after successfully joining the domain.

## 4. Verify Domain Membership

After the restart, domain membership was verified using:

```powershell
Get-CimInstance Win32_ComputerSystem |
    Select-Object Name, Domain, PartOfDomain
```

Verified result:

| Property | Value |
|---|---|
| Computer Name | DC02 |
| Domain | lab.local |
| PartOfDomain | True |

## 5. Result

DC02 successfully joined the existing Active Directory domain `lab.local`.

The server is now a domain member and ready for the installation of the Active Directory Domain Services (AD DS) and DNS roles.
