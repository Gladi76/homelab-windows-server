# Windows Server Homelab – IT Infrastructure Project

## Overview

This repository documents my practical Windows Server homelab project.

The goal of the project is to build, configure and administer a small enterprise-style IT infrastructure using Microsoft Windows Server, Active Directory and Hyper-V.

The environment is continuously extended and documented with configuration steps, verification procedures, screenshots and troubleshooting examples.

## Infrastructure

The lab environment is based on Microsoft Hyper-V and Windows Server 2022.

### Server Environment

| System | Role | IP Address |
|---|---|---|
| DC01 | Primary Domain Controller, AD DS, DNS | `192.168.178.230` |
| DC02 | Additional Domain Controller, AD DS, DNS | `192.168.178.231` |
| DHCP01 | DHCP Server | `192.168.178.232` |
| FILE01 | File Server | `192.168.178.236` |
| CLIENT02 | Windows Client | `192.168.178.240` |

### Active Directory

Domain:

```text
lab.local
```

The Active Directory environment includes:

- Domain Controllers
- Organizational Units
- User accounts
- Security groups
- Computer accounts
- Group Policy Objects (GPOs)
- DNS integration
- Domain authentication

## Technologies & Skills

### Microsoft Infrastructure

- Windows Server 2022
- Active Directory Domain Services (AD DS)
- DNS Server
- DHCP Server
- Group Policy (GPO)
- Active Directory Users and Computers
- Hyper-V
- Windows Server File Services

### File Server

- NTFS permissions
- SMB shares
- Active Directory security groups
- Department-based access control
- Permission verification
- User access testing

### Networking

- IPv4
- DNS
- DHCP
- TCP/IP
- Network connectivity testing
- Domain Controller discovery

### Troubleshooting & Administration

- Windows Server administration
- Active Directory troubleshooting
- DNS troubleshooting
- Domain authentication troubleshooting
- Group Policy verification
- PowerShell and Windows command-line tools
- Practical access and connectivity testing

## Project Structure

```text
homelab-windows-server/
│
├── 01-hyper-v/
├── 02-domain-controller-dc01/
├── 03-domain-controller-dc02/
├── 04-dns-configuration/
├── 05-active-directory-management/
│   ├── 01-user-and-computer-management.md
│   ├── 02-group-policy-management.md
│   └── 03-gpo-verification.md
├── 06-file-server/
├── 07-dhcp-server/
│
└── README.md
```

## Active Directory Management

The Active Directory environment contains separate Organizational Units for departments such as HR and IT.

Example users:

| User | Department | Security Group |
|---|---|---|
| Hans Wurst | HR | `LAB\HR` |
| Max Mustermann | IT | `LAB\IT` |

Security groups are used to manage access to department resources instead of assigning permissions directly to individual users.

## File Server

FILE01 provides separate network shares for the HR and IT departments.

```text
FILE01
└── E:\Shares
    ├── HR
    └── IT
```

Access is controlled using a combination of:

- Active Directory security groups
- NTFS permissions
- SMB share permissions

Practical access tests confirmed that users can access their own department share while access to the other department's share is denied.

## Group Policy

Group Policy is used to manage Windows settings centrally within the Active Directory environment.

The project includes:

- GPO creation
- Domain and OU-based policy management
- Password and account lockout policies
- Policy application
- GPO verification on CLIENT02

## Verification & Troubleshooting

The environment is tested after configuration changes to verify that services and permissions work as intended.

Examples include:

- Domain Controller connectivity
- DNS resolution
- DHCP configuration
- Domain authentication
- Secure channel verification
- SMB access testing
- NTFS permission testing
- Group Policy application
- Department-level access restrictions

Troubleshooting is documented together with the investigation steps and the final resolution.

## Project Goals

This project demonstrates practical experience with:

- Windows Server administration
- Active Directory
- DNS and DHCP
- Group Policy
- Hyper-V virtualization
- File server administration
- NTFS and SMB permissions
- Network troubleshooting
- User and computer management
- Documentation of IT infrastructure

## Documentation

Each infrastructure component is documented separately with configuration steps, verification procedures and screenshots.

The project is continuously updated as additional services and administration tasks are implemented.

## Author

**IT System Administration Homelab Project**

Focus:

**Windows Server · Active Directory · Microsoft Azure · Networking · Virtualization · Cloud & On-Premises Infrastructure**

## Planned Extensions (Roadmap)
* [ ] Hybrid Identity integration with **Microsoft Entra ID** via **Entra Connect** (planned next step)
* [ ] Administration and device management of **Microsoft 365** services (**Intune, Exchange Online, Teams, Outlook, SharePoint**) integrated within a **Hybrid Cloud environment**
* [ ] Centralized monitoring and alerting integration
