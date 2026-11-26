# FILE01 – Folder Structure

## 1. Overview

This section documents the directory structure of the FILE01 file server.

A separate data disk (E:) is used to store shared files and department data. This keeps user data separate from the Windows Server operating system.

## 2. Storage Layout

| Drive | Purpose |
|---|---|
| C: | Windows Server operating system |
| E: | File server data |

The main directory for shared data is:

```text
E:\Shares
```

## 3. Department Folder Structure

The following department folders have been created:

```text
E:\
└── Shares
    ├── HR
    └── IT
```

| Folder | Purpose |
|---|---|
| `E:\Shares\HR` | Files and documents for the Human Resources department |
| `E:\Shares\IT` | Files and documents for the IT department |

## 4. Access Management Concept

Access to the department folders will be managed through Active Directory security groups.

| Folder | Active Directory Group |
|---|---|
| `HR` | `LAB\HR` |
| `IT` | `LAB\IT` |

Users are assigned to their respective department groups in Active Directory.

Permissions will be configured separately in the next steps.

## 5. Screenshots

### Department Folder Structure

The screenshot shows the directory structure on the separate data disk of FILE01.

<img width="935" height="432" alt="image" src="https://github.com/user-attachments/assets/2e76f4a9-2047-404a-9152-1cc8f97d1e3f" />

## 6. Current Status

- Separate data disk E: available
- Main directory `E:\Shares` created
- HR department folder created
- IT department folder created
- Active Directory security groups prepared

## Next Step

Configure NTFS permissions for the HR and IT department folders using the Windows graphical interface.
