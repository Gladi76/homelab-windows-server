# Windows Server Homelab – IT Infrastructure Project

## Overview
This repository documents my practical Windows Server homelab environment. The objective of this project is to design, deploy, configure, and administer a small enterprise-style IT infrastructure using **Microsoft Windows Server 2022**, **Active Directory**, and **Hyper-V**.

The environment is continuously expanded and documented with step-by-step configurations, verification procedures, architectural notes, and real-world troubleshooting examples.

---

## Infrastructure & Network Topology

The lab runs on **Microsoft Hyper-V** within a dedicated local network segment (`192.168.178.0/24`). Redundancy and service separation follow standard enterprise design principles.

### Server Environment

| System | Role | OS / Platform | IP Address |
| :--- | :--- | :--- | :--- |
| **DC01** | Primary Domain Controller, AD DS, DNS | Windows Server 2022 | `192.168.178.230` |
| **DC02** | Additional Domain Controller, AD DS, DNS | Windows Server 2022 | `192.168.178.231` |
| **DHCP01** | Dedicated DHCP Server | Windows Server 2022 | `192.168.178.232` |
| **FILE01** | File Server (SMB / NTFS Shares) | Windows Server 2022 | `192.168.178.236` |
| **CLIENT02** | Domain-Joined Workstation (Testing & GPO Verification) | Windows 10 / 11 Pro | `192.168.178.240` |

### Active Directory Domain
* **Internal Lab Domain:** `lab.local`
* **Core Components:**
  * Multi-DC architecture (`DC01` & `DC02`) with AD-integrated DNS and replication
  * Structured Organizational Units (OUs) by department and device type
  * Role-Based Access Control (RBAC) via AD Security Groups
  * Centralized configuration management using Group Policy Objects (GPOs)

---

## Technologies & Core Skills

* **Microsoft Infrastructure:** Windows Server 2022, Active Directory Domain Services (AD DS), DNS, DHCP, Group Policy (GPO), Hyper-V, Windows File Services
* **Storage & Access Control:** NTFS Permissions, SMB Shares, Security Group Delegation, Least-Privilege Principle
* **Networking:** IPv4 Subnetting, TCP/IP, DNS Name Resolution, DHCP Scope Management, Domain Controller Discovery
* **Administration & Troubleshooting:** PowerShell, Windows CLI Diagnostics, Event Viewer Analysis, Secure Channel & Replication Verification

---

## Repository Structure

```text
homelab-windows-server/
│
├── 01-hyper-v/                       # Virtualization host setup, virtual switches, VM provisioning
├── 02-domain-controller-dc01/        # AD DS installation, forest/domain creation, primary DNS
├── 03-domain-controller-dc02/        # Domain controller promotion, AD & DNS replication
├── 04-dns-configuration/             # Forward/Reverse lookup zones, conditional forwarders
├── 05-active-directory-management/   # OUs, user/computer administration, and GPO rollout
│   ├── 01-user-and-computer-management.md
│   ├── 02-group-policy-management.md
│   └── 03-gpo-verification.md
├── 06-file-server/                   # SMB shares, NTFS permissions, and access testing
├── 07-dhcp-server/                   # DHCP scopes, reservations, and failover/lease verification
│
└── README.md 

## Planned Extensions (Roadmap)
* [ ] Hybrid Identity integration with **Microsoft Entra ID** via **Entra Connect** (planned next step)
* [ ] Automated server baseline deployment and configuration via **PowerShell / Ansible**
* [ ] Centralized monitoring and alerting integration

---

## Author
**Mohanad Alshehawi** – IT System Administrator  
**Focus:** Windows Server · Active Directory · Networking · Virtualization · On-Premises & Cloud Infrastructure
