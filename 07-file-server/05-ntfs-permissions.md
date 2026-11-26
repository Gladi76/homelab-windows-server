# FILE01 – NTFS Permissions

## 1. Overview

This section documents the NTFS permissions configured on the FILE01 file server.

Access to department folders is managed through Active Directory security groups.

## 2. Folder Structure

The following folders are used:

```text
E:\Shares
├── HR
└── IT
```

## 3. NTFS Permission Configuration

The following permissions were configured:

| Folder | Security Group | Permission | Applies To |
|---|---|---|---|
| `E:\Shares\HR` | `LAB\HR` | Modify | This folder, subfolders and files |
| `E:\Shares\IT` | `LAB\IT` | Modify | This folder, subfolders and files |

The Modify permission allows members of the respective department group to read, create, modify and delete files and folders.

## 4. Active Directory Group Membership

The following users are assigned to their department groups:

| User | Account | Group |
|---|---|---|
| Hans Wurst | `h.wurst` | `LAB\HR` |
| Max Mustermann | `m.mustermann` | `LAB\IT` |

## 5. Permission Management

NTFS permissions were configured using the Windows graphical interface:

1. Open the folder properties.
2. Select **Security**.
3. Open **Advanced Security Settings**.
4. Add the respective Active Directory security group.
5. Assign **Modify** permissions.
6. Apply the permissions to the folder, subfolders and files.

## 6. Screenshots

### HR Folder – NTFS Permissions

The screenshot shows the NTFS permissions assigned to `LAB\HR` on `E:\Shares\HR`.
<img width="850" height="587" alt="Screenshot 2026-11-25 130538" src="https://github.com/user-attachments/assets/6813d30b-f1ee-4e86-addb-bbee08c37238" />


### IT Folder – NTFS Permissions

The screenshot shows the NTFS permissions assigned to `LAB\IT` on `E:\Shares\IT`.
<img width="828" height="509" alt="Screenshot 2026-11-25 130251" src="https://github.com/user-attachments/assets/12c76fe4-dffd-4eb5-b5e8-ea19e32d650c" />


## 7. Result

- NTFS permissions configured for the HR folder.
- NTFS permissions configured for the IT folder.
- Department access managed through Active Directory security groups.
- Modify permissions assigned to the respective department groups.

## Next Step

Configure and document the SMB network shares for HR and IT.
