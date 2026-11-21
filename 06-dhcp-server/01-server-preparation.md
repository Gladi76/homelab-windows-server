# DHCP Server – Server Preparation

## 1. Objective

This section documents the creation of a dedicated virtual machine for the DHCP Server in the Windows Server home lab.

The DHCP service runs on a separate server to keep infrastructure services organized and independent from the domain controllers.

## 2. Virtual Machine Creation

A new virtual machine was created using Microsoft Hyper-V.

| Configuration | Value |
|---|---|
| VM Name | DHCP01 |
| Hypervisor | Microsoft Hyper-V |
| Generation | Generation 2 |
| Virtual Processors | 4 vCPUs |
| Assigned Memory | 4096 MB |
| Virtual Hard Disk | 127 GB |
| Operating System | Windows Server 2022 |
| Server Role | DHCP Server |

## 3. Windows Server Installation

Windows Server 2022 was installed on the newly created virtual machine using the installation media.

After installation, the server was started and the initial Windows Server setup was completed.

## 4. Centralized Server Management

The DHCP01 server was added to Server Manager on DC01 using the **Add Servers** feature.

This allows centralized administration and monitoring of the servers from DC01.

The following servers are registered in Server Manager:

| Server | IPv4 Address | Status |
|---|---|---|
| DC01 | 192.168.178.230 | Online |
| DC02 | 192.168.178.231 | Online |
| DHCP01 | 192.168.178.232 | Online |
| FILE01 | 192.168.178.236 | Online |

All four servers are displayed as online in Server Manager.

## 5. Initial Server Status

| Item | Status |
|---|---|
| Virtual Machine | Created |
| Windows Server 2022 | Installed |
| Server Name | DHCP01 |
| IPv4 Address | 192.168.178.232 |
| Added to Server Manager on DC01 | Yes |
| DHCP Role | Not yet installed |

## 6. Screenshots
<img width="950" height="380" alt="image" src="https://github.com/user-attachments/assets/e62a49f9-061d-42c2-a54f-95de33cfa1b9" />

## 7. Result

The DHCP01 virtual machine was successfully created and Windows Server 2022 was installed.

The server was added to Server Manager on DC01 and is displayed as online alongside DC01, DC02 and FILE01.

The next step is to document the network configuration and domain membership of DHCP01.
