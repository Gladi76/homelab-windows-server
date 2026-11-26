# Active Directory – User and Computer Management

## 1. Overview

This section documents the management of users, security groups and computer objects in the Active Directory domain `lab.local`.

User and computer accounts are organized using Organizational Units (OUs) to simplify administration and apply centralized policies.

## 2. Organizational Unit Structure

The following Organizational Units are used:

| Organizational Unit | Purpose |
|---|---|
| HR | Human Resources department |
| IT | Information Technology department |
| Domain Controllers | Domain controller computer accounts |

## 3. User Accounts

The following domain user accounts were created:

| User | Username | Organizational Unit |
|---|---|---|
| Hans Wurst | `h.wurst` | HR |
| Max Mustermann | `m.mustermann` | IT |

User accounts are managed centrally through Active Directory Users and Computers.

## 4. Security Groups

Department access is managed through Global Security Groups.

| Group | Group Scope | Group Type | Department |
|---|---|---|---|
| HR | Global | Security | Human Resources |
| IT | Global | Security | Information Technology |

The corresponding users were assigned to their department groups:

- Hans Wurst → `LAB\HR`
- Max Mustermann → `LAB\IT`

These groups are used to manage access to the department folders on FILE01.

## 5. Computer Objects

The following infrastructure systems are part of the domain environment:

| Computer | Role |
|---|---|
| DC01 | Primary Domain Controller |
| DC02 | Additional Domain Controller |
| FILE01 | File Server |
| DHCP01 | DHCP Server |
| CLIENT02 | Domain Client |

Computer accounts are managed centrally in Active Directory.

## 6. Administration

The graphical management console used for administration is:

**Server Manager → Tools → Active Directory Users and Computers**

The console allows administrators to:

- Create and manage user accounts.
- Organize objects in Organizational Units.
- Create and manage security groups.
- Assign users to security groups.
- Manage domain computer accounts.

## 7. Screenshots

The following screenshots can be added:

- Active Directory Organizational Units
- HR user account
- IT user account
- HR and IT security groups with their members
- Domain computer objects

<img width="886" height="264" alt="Screenshot 2026-11-26 085548" src="https://github.com/user-attachments/assets/73225014-4f35-471e-b5a9-ca52542b4a28" />
<img width="880" height="253" alt="image" src="https://github.com/user-attachments/assets/24370f68-4fde-4331-b465-6bd1d87ad02f" />

## 8. Result

- HR and IT Organizational Units configured.
- Department user accounts created.
- Global Security Groups created.
- Users assigned to their corresponding security groups.
- Domain computer objects managed centrally.
- Active Directory structure prepared for centralized Group Policy management.

## Next Step

Configure Group Policy Objects (GPOs) to manage security and Windows settings centrally.
