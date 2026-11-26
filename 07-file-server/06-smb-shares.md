# FILE01 – SMB Shares

## 1. Overview

This section documents the SMB network shares configured on FILE01.

The department folders are shared over the network so that authorized domain users can access their department files.

## 2. SMB Share Configuration

The following SMB shares were created:

| Share Name | Local Folder | Network Path |
|---|---|---|
| HR | `E:\Shares\HR` | `\\FILE01\HR` |
| IT | `E:\Shares\IT` | `\\FILE01\IT` |

## 3. SMB Share Permissions

Access to each share is restricted to the corresponding Active Directory security group.

| Share | Security Group | Permission |
|---|---|---|
| HR | `LAB\HR` | Change |
| IT | `LAB\IT` | Change |

The default `Everyone` (`Jeder`) entry was removed from both shares.

## 4. Permission Verification

SMB share permissions were verified using PowerShell:

```powershell
Get-SmbShareAccess -Name "HR","IT" |
    Format-Table Name, AccountName, AccessControlType, AccessRight -AutoSize
```

The output confirmed:

- HR: `LAB\HR` – Allow – Change
- IT: `LAB\IT` – Allow – Change

The following command was also used to check for remaining `Everyone` or `Jeder` entries:

```powershell
Get-SmbShareAccess -Name "HR","IT" |
    Where-Object AccountName -Match "Everyone|Jeder"
```

No matching entries were returned.

## 5. Access Management

SMB share permissions and NTFS permissions work together to control network access.

The effective access is restricted by both permission layers.

- SMB permissions control access through the network share.
- NTFS permissions control access to files and folders on the file system.

Both permission layers must allow the requested operation.

## 6. Screenshots

### HR SMB Share Permissions

The screenshot shows the SMB share permissions configured for the HR share. Only the `LAB\HR` security group has Change access.
<img width="812" height="510" alt="image" src="https://github.com/user-attachments/assets/fab3b62c-ae65-4b36-87f6-eeb8a4da7b4e" />

### IT SMB Share Permissions

The screenshot shows the SMB share permissions configured for the IT share. Only the `LAB\IT` security group has Change access.
<img width="767" height="496" alt="image" src="https://github.com/user-attachments/assets/4694fa6c-7a60-4969-af8d-e39a72578871" />

### PowerShell Verification

The screenshot shows the PowerShell output confirming the SMB share permissions for both shares.
<img width="1121" height="508" alt="Screenshot 2026-11-25 134837" src="https://github.com/user-attachments/assets/341952f8-0502-4503-8efd-97b321f95447" />

## 7. Result

- HR and IT SMB shares successfully created.
- Access restricted to the corresponding Active Directory security groups.
- `Everyone` (`Jeder`) removed from both share permission
