# FILE01 – Server Preparation 

## Project Overview

This section documents the preparation of the FILE01 virtual machine for the Windows Server 2022 file server role.

## Virtual Machine

| Configuration | Value |
|---|---|
| VM Name | FILE01 |
| Hypervisor | Microsoft Hyper-V |
| Operating System | Windows Server 2022 Datacenter |
| Generation | Generation 2 |
| Virtual Processors | 4 |
| Memory | 4096 MB |
| System Disk | 127 GB |
| Data Disk | 100 GB |
| Role | File Server |

## Network Configuration

FILE01 was configured with a static IPv4 address and joined to the existing Active Directory domain.

| Configuration | Value |
|---|---|
| Hostname | FILE01 |
| Domain | lab.local |
| IPv4 Address | 192.168.178.236 |
| DNS Server | 192.168.178.230 |

## Separate Data Disk

A separate virtual disk was added for file server data.

The purpose of the additional disk is to keep user and department data separate from the Windows operating system.

```text
C:\  → Windows Server operating system
E:\  → File server data
```

The additional disk was detected and configured as follows:

| Configuration | Value |
|---|---|
| Disk | Disk 1 |
| Size | 100 GB |
| Partition Style | GPT |
| Drive Letter | E: |
| File System | NTFS |
| Health Status | Healthy |
| Operational Status | OK |

## Data Directory

The main directory for shared file server data is:

```text
E:\Shares
```

Department-specific folders will be created below this directory.

## Domain Membership

FILE01 is a member of the Active Directory domain:

```text
lab.local
```

The computer secure channel was verified successfully.

## Status

- FILE01 virtual machine created
- Windows Server 2022 installed
- Static IP configured
- FILE01 joined to `lab.local`
- Additional 100 GB data disk configured
- Data disk formatted with NTFS
- `E:\Shares` prepared as the main data directory

## Next Step

Install the Windows Server **File Server** role on FILE01.
