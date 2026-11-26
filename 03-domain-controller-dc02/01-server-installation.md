# DC02 – Windows Server Installation

## 1. Objective

This step describes the installation and initial preparation of a second Windows Server 2022 virtual machine.

DC02 will be configured as an additional Domain Controller for the existing Active Directory domain `lab.local`.

The server is installed using the Server Core installation option.

## 2. Virtual Machine Configuration

The virtual machine was created in Hyper-V with the following configuration:

| Setting | Value |
|---|---|
| Computer Name | DC02 |
| Operating System | Windows Server 2022 Datacenter |
| Installation Type | Server Core |
| Generation | Generation 2 |
| Virtual Processors | 4 vCPUs |
| Memory | 4096 MB |
| Virtual Hard Disk | 127 GB |
| Network | External Virtual Switch |

## 3. Operating System Verification

After installation, the Windows Server version was verified using PowerShell.

```powershell
Get-ComputerInfo | Select-Object WindowsProductName, WindowsVersion, OsBuildNumber
```

System information:

- Windows Server 2022 Datacenter
- Version 2009
- OS Build 20348

## 4. Rename the Server

The automatically generated computer name was changed to `DC02`.

```powershell
Rename-Computer -NewName "DC02" -Restart
```

The server restarted to apply the new computer name.

## 5. Result

DC02 was successfully installed with Windows Server 2022 Datacenter Server Core and prepared for the network configuration and domain integration.

## 6. Screenshot

<img width="994" height="528" alt="Screenshot 2026-11-19 234551" src="https://github.com/user-attachments/assets/adba9eb9-2213-4896-969c-8f5a04b01118" />
<img width="990" height="519" alt="image" src="https://github.com/user-attachments/assets/d249b1e5-87ba-482e-8f43-6d0e08f66cb0" />

