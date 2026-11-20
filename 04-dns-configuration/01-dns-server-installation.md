# DNS Server Installation on DC02

## 1. Objective

Install and configure the DNS Server role on DC02.

DNS is an essential component of Active Directory. It enables Domain Controller discovery, name resolution and communication between domain members.

## 2. Install DNS Server

The DNS Server role was installed using PowerShell:

```powershell
Install-WindowsFeature DNS -IncludeManagementTools
```

## 3. Verify Installation

The installed role was checked using:

```powershell
Get-WindowsFeature DNS
```

The DNS Server role was successfully installed.

## 4. Remote DNS Management

The DNS Manager console on DC01 was used to manage the DNS Server on DC02.

The remote server was added using:

**Server Manager → Tools → DNS → Add DNS Server**

The hostname `DC02` was entered to establish the connection.

## 5. Result

DC02 has the DNS Server role installed and can be administered remotely from DC01.

## 6. Screenshot

The screenshot below shows the DNS role installation.

![DNS Server role installation](https://github.com/user-attachments/assets/823c67b6-5145-4429-9b45-bd8290c9a411)
