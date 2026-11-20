# DC02 – Domain Controller Promotion

## 1. Objective

Promote DC02 to an additional Domain Controller in the existing Active Directory domain `lab.local`.

DC01 is the existing Domain Controller and acts as the replication source.

## 2. Promotion Configuration

The following configuration was used:

| Setting | Value |
|---|---|
| Domain | lab.local |
| New Domain Controller | DC02 |
| Replication Source | DC01.lab.local |
| DNS Server | Installed on DC02 |
| Global Catalog | Enabled |
| Read-Only Domain Controller | No |
| Active Directory Site | Leipzig |

## 3. Configure the DSRM Password

A Directory Services Restore Mode (DSRM) password was entered securely using PowerShell.

```powershell
$DSRMPassword = Read-Host "Enter DSRM password" -AsSecureString
```

**Security note:** The DSRM password is confidential and must never be stored in a public repository.

## 4. Promote DC02

The following PowerShell command was used to promote DC02:

```powershell
Install-ADDSDomainController `
    -DomainName "lab.local" `
    -InstallDns `
    -Credential $Credential `
    -ReplicationSourceDC "DC01.lab.local" `
    -SiteName "Leipzig" `
    -SafeModeAdministratorPassword $DSRMPassword `
    -NoGlobalCatalog:$false `
    -Force
```

The promotion completed successfully and the server restarted automatically.

## 5. Verify Domain Controller Promotion

After restarting, the new Domain Controller was checked:

```powershell
Get-ADDomainController -Identity DC02
```

The following properties were verified:

| Property | Result |
|---|---|
| Hostname | DC02.lab.local |
| IPv4 Address | 192.168.178.231 |
| Domain | lab.local |
| Forest | lab.local |
| Enabled | True |
| Global Catalog | True |
| Read-Only | False |
| Operating System | Windows Server 2022 Datacenter |

DC02 is now an additional writable Domain Controller.

## 6. Result

DC02 was successfully promoted as an additional Domain Controller in the existing Active Directory domain.

Active Directory and DNS services are installed, and DC02 is configured as a Global Catalog server.

## 7. Screenshot

<img width="1002" height="523" alt="Screenshot 2026-11-20 004408" src="https://github.com/user-attachments/assets/932c147f-3922-4564-8826-0765322bc0b8" />

