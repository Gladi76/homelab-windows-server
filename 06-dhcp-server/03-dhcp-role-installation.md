# DHCP Server – Role Installation

## 1. Objective

This section documents the installation of the DHCP Server role on the dedicated Windows Server 2022 virtual machine.

The DHCP service is installed on DHCP01 as a separate infrastructure service within the Active Directory domain `lab.local`.

## 2. Server Information

| Configuration    | Value               |
| ---------------- | ------------------- |
| Server Name      | DHCP01              |
| FQDN             | DHCP01.lab.local    |
| Operating System | Windows Server 2022 |
| IPv4 Address     | 192.168.178.232     |
| Domain           | lab.local           |
| Server Role      | DHCP Server         |

## 3. DHCP Server Role Installation

The DHCP Server role was installed using Server Manager.

The following steps were performed:

1. Open **Server Manager**.
2. Select **Manage**.
3. Click **Add Roles and Features**.
4. Select **Role-based or feature-based installation**.
5. Select the target server `DHCP01`.
6. Select **DHCP Server** under Server Roles.
7. Confirm the required management tools.
8. Click **Next** and proceed through the wizard.
9. Click **Install** to start the installation.

After the installation was completed, the DHCP Server role was available on DHCP01.

## 4. DHCP Management Tools

The DHCP management tools were installed together with the DHCP Server role.

They allow the administrator to manage DHCP scopes, address leases, reservations and server options.

The DHCP management console can be opened through:

**Server Manager → Tools → DHCP**

## 5. Installation Verification

The DHCP Server service can be checked using PowerShell:

```powershell
Get-Service DHCPServer
```

Expected result:

```text
Status   Name        DisplayName
------   ----        -----------
Running  DHCPServer  DHCP Server
```

The installed DHCP role can also be checked using:

```powershell
Get-WindowsFeature DHCP
```

Expected result:

```text
Display Name             Name   Install State
------------             ----   -------------
[X] DHCP Server          DHCP   Installed
```

## 6. Screenshots

The following screenshots will document the installation:

- Add Roles and Features wizard
- DHCP Server role selection
- Installation completed
- DHCP Server management console
- PowerShell installation verification
<img width="787" height="505" alt="Screenshot 2026-11-20 224655" src="https://github.com/user-attachments/assets/bea6bcd4-e9b0-45a5-a350-dd6247a800aa" />
<img width="782" height="551" alt="Screenshot 2026-11-20 224819" src="https://github.com/user-attachments/assets/a351c04d-beb8-4dd0-9fe9-5c7b5842e09d" />
<img width="780" height="553" alt="Screenshot 2026-11-20 225002" src="https://github.com/user-attachments/assets/5e543470-9d57-40c9-80ab-60f96e27d2bb" />
<img width="961" height="509" alt="image" src="https://github.com/user-attachments/assets/f66d8215-1777-4516-b65f-382495520e43" />

## 7. Result

The DHCP Server role and its management tools were installed on DHCP01.

The server is now prepared for authorization in Active Directory.

The next step is to authorize DHCP01 in Active Directory before configuring and activating the DHCP scope.
