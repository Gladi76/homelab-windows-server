# FILE01 – File Server Role Installation

## Overview

FILE01 is used as the dedicated file server for the `lab.local` environment.

The Windows Server **File Server** role was installed before configuring the file shares and access permissions.

## File Server Role

The installed Windows Server role is:

```text
File Server
```

PowerShell was used to verify the installation:

```powershell
Get-WindowsFeature FS-FileServer
```

The installation state was confirmed as:

```text
[X] File Server
    FS-FileServer
    Installed
```

## Installation

The File Server role was installed using PowerShell:

```powershell
Install-WindowsFeature FS-FileServer -IncludeManagementTools
```

The installation completed successfully.

The server did not require a restart after the installation.

## Data Storage

The file server uses a separate data disk for shared files:

```text
C:\  → Operating system
E:\  → File server data
```

The main directory is:

```text
E:\Shares
```

Department folders will be created below this directory.

## Planned File Server Structure

The planned structure is:

```text
E:\Shares
├── HR
└── IT
```

Access to these folders will later be controlled through Active Directory security groups.

## Active Directory Groups

The following security groups have been created in Active Directory:

| Group | Purpose |
|---|---|
| `HR` | Access control for the HR department |
| `IT` | Access control for the IT department |

The groups are configured as **Global Security Groups**.

## Screenshots

### 1. File Server Role Installation

The File Server role was selected and installed through Server Manager.

<img width="780" height="553" alt="image" src="https://github.com/user-attachments/assets/449087fd-5bb8-4896-aad6-1d0cc945b378" />

### 2. File Server Role Verification

The installation was verified using PowerShell.
<img width="959" height="510" alt="image" src="https://github.com/user-attachments/assets/62c20e52-af50-4a65-a605-4fab0378d98c" />


## Status

- File Server role installed successfully
- File Server management tools installed
- No restart required
- Separate data disk available
- `E:\Shares` available
- Active Directory security groups `HR` and `IT` prepared

## Next Step

Document the basic concepts of Windows file server permissions, including:

- Access Control List (ACL)
- Access Control Entry (ACE)
- NTFS permissions
- SMB share permissions
- Permission inheritance
- Effective access
