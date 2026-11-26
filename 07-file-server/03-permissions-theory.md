# File Server Permissions – Theory

## Overview

A Windows file server uses several security mechanisms to control access to files and folders.

For this lab, the main concepts are:

- Access Control List (ACL)
- Access Control Entry (ACE)
- NTFS permissions
- SMB share permissions
- Effective permissions
- Security groups

Understanding these concepts is important before configuring the file server.

---

## 1. Access Control List (ACL)

An **Access Control List (ACL)** is a list of permissions associated with a securable Windows object, such as a file or folder.

The ACL defines **who** can access the object and **what they are allowed to do**.

Example:

```text
E:\Shares\HR
│
└── ACL
    ├── LAB\HR       → Modify
    ├── Administrators → Full Control
    └── SYSTEM         → Full Control
```

The ACL itself is not a single permission. It is a collection of individual permission entries.

---

## 2. Access Control Entry (ACE)

An **Access Control Entry (ACE)** is one individual entry inside an ACL.

For example:

```text
LAB\HR → Modify
```

is one ACE.

A folder can therefore contain multiple ACEs:

```text
ACL
│
├── ACE: LAB\HR → Modify
├── ACE: Administrators → Full Control
└── ACE: SYSTEM → Full Control
```

In simple terms:

> **ACL = the complete permission list**

> **ACE = one entry inside that list**

---

## 3. NTFS Permissions

NTFS permissions control access to files and folders on an NTFS-formatted disk.

Typical NTFS permissions include:

- Full Control
- Modify
- Read & Execute
- List Folder Contents
- Read
- Write

For this lab, we use **Modify** for department users.

Example:

```text
E:\Shares\HR
    ↓
LAB\HR
    ↓
Modify
```

This allows members of the HR group to create, modify and delete files within the HR folder.

---

## 4. Why Use Security Groups?

Users should normally not be assigned permissions individually.

Instead, permissions are assigned to security groups.

Example:

```text
User
Hans Wurst
     │
     ▼
Group
LAB\HR
     │
     ▼
NTFS Permission
Modify
     │
     ▼
E:\Shares\HR
```

This makes permission management easier.

If another employee joins the HR department, the administrator only needs to add the new user to the `LAB\HR` group.

The folder permissions do not have to be changed.

---

## 5. Global Security Groups

In this lab, the department groups are configured as:

```text
HR → Global Security Group
IT → Global Security Group
```

The users are members of their respective groups:

```text
LAB\HR
└── Hans Wurst

LAB\IT
└── Max Mustermann
```

The groups are then used when configuring access to the file server.

---

## 6. SMB Share Permissions

NTFS permissions are not the only permissions involved when a folder is accessed over the network.

Windows file sharing uses **SMB (Server Message Block)**.

For example:

```text
\\FILE01\HR
```

has SMB share permissions in addition to NTFS permissions.

The access path is therefore:

```text
Client
  │
  │ SMB
  ▼
SMB Share
  │
  ▼
NTFS Permissions
  │
  ▼
Folder / File
```

---

## 7. NTFS vs. SMB Permissions

When a user accesses a shared folder over the network, both permission layers can apply.

Example:

```text
SMB Permission:
LAB\HR → Change

NTFS Permission:
LAB\HR → Modify
```

The effective access is determined by the combination of the applicable permissions.

A useful rule for this lab is:

> **The most restrictive effective permission determines the final access.**

For example:

```text
SMB:  Read
NTFS: Modify
----------------
Effective: Read
```

Therefore, giving a user `Modify` through NTFS does not help if the SMB share only allows Read access.

---

## 8. Share Permissions vs. NTFS Permissions

For this lab, we keep the configuration simple and easy to understand.

The SMB share provides the network-level access, while NTFS provides the detailed file-system permissions.

Example:

```text
\\FILE01\HR
      │
      ├── SMB Permission
      │
      └── NTFS Permission
             │
             └── LAB\HR → Modify
```

This separation makes it easier to understand where access is controlled.

---

## 9. Inheritance

Windows NTFS permissions can be inherited from a parent folder.

For example:

```text
E:\Shares
    │
    ├── HR
    │    └── files
    │
    └── IT
         └── files
```

Permissions configured on `E:\Shares` can potentially be inherited by `HR` and `IT`.

Inheritance can be useful, but it must be configured carefully.

For department-specific folders, unnecessary inherited permissions can give users access to folders they should not see.

---

## 10. Effective Access

The final access a user receives can depend on several factors:

- Direct user permissions
- Group membership
- NTFS permissions
- SMB permissions
- Inherited permissions
- Explicit Deny permissions

For example:

```text
Hans Wurst
     │
     └── Member of LAB\HR
              │
              ▼
       NTFS: Modify
              │
              ▼
         E:\Shares\HR
```

When troubleshooting access problems, it is therefore important to check the complete permission path.

---
## 11. Deny Permissions and Permission Precedence

Windows NTFS permissions support both **Allow** and **Deny** access control entries (ACEs).

When a user receives conflicting permissions through direct assignments and group memberships, an applicable explicit Deny ACE generally takes precedence over an Allow ACE.

### Example

Assume that:

- Hans Wurst is a member of the `HR` security group.
- The `HR` group has **Modify (Allow)** permission on `E:\Shares\HR`.
- Hans Wurst receives an explicit **Delete (Deny)** permission on the same folder.

The result is:

| Permission | Assigned To | Result |
|---|---|---|
| Modify (Allow) | HR group | Allowed |
| Delete (Deny) | Hans Wurst | Denied |

The explicit Deny entry blocks the specified operation, even though the user receives Allow permissions through group membership.

### Important Note

Deny permissions should be used carefully because they can override permissions granted through security group membership and make access management more complex.

**Best practice:** Prefer assigning Allow permissions through Active Directory security groups. Use explicit Deny permissions only when there is a clear requirement.

## 12. Permission Design for This Lab

The planned configuration is:

| Folder | AD Group | NTFS Permission |
|---|---|---|
| `E:\Shares\HR` | `LAB\HR` | Modify |
| `E:\Shares\IT` | `LAB\IT` | Modify |

Users:

| User | Group |
|---|---|
| Hans Wurst | `LAB\HR` |
| Max Mustermann | `LAB\IT` |

This creates a simple role-based permission model.

```text
Hans Wurst
    │
    ▼
 LAB\HR
    │
    ▼
E:\Shares\HR
    │
    └── Modify


Max Mustermann
    │
    ▼
 LAB\IT
    │
    ▼
E:\Shares\IT
    │
    └── Modify
```

---

## 13. Key Concepts

| Concept | Meaning |
|---|---|
| ACL | Complete list of access permissions |
| ACE | Individual permission entry inside an ACL |
| NTFS | Windows file system with file/folder permissions |
| SMB | Protocol used for Windows network file sharing |
| Security Group | Group used to assign permissions to multiple users |
| Inheritance | Permissions passed from a parent object to child objects |
| Effective Access | The access a user actually receives |

---

## Conclusion

The FILE01 configuration uses **Active Directory security groups** to manage access to department folders.

Instead of assigning permissions directly to individual users, permissions are assigned to groups:

```text
User → Security Group → NTFS Permission → Folder
```

This approach makes the file server easier to manage, scale and troubleshoot.
