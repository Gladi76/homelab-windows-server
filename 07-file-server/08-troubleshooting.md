# FILE01 – Troubleshooting

## 1. Overview

This section documents troubleshooting activities performed during the configuration and testing of the Windows Server 2022 file server environment.

The focus is on domain connectivity, DNS configuration and access permissions.

## 2. Domain Login Issue on CLIENT02

### Problem

During testing, the following error appeared when attempting to sign in with a domain account:

```text
We can't sign you in with this credential because your domain isn't available.
```

CLIENT02 was already joined to the Active Directory domain `lab.local`, but domain authentication initially failed.

### Investigation

The following checks were performed:

- Checked the client's IPv4 configuration.
- Identified that the client initially received its network configuration from the Fritz!Box instead of the Windows DHCP server.
- Renewed the DHCP configuration using:

```powershell
ipconfig /renew
```

### Verification

After renewing the configuration, CLIENT02 received the expected network settings:

| Configuration | Value |
|---|---|
| IP Address | 192.168.178.240 |
| DHCP Server | 192.168.178.232 |
| Preferred DNS | 192.168.178.230 |
| Alternate DNS | 192.168.178.231 |

The following commands were used to verify connectivity and domain discovery:

```powershell
Test-NetConnection DC01 -Port 389
Test-NetConnection DC02 -Port 389
```

```powershell
nslookup DC01.lab.local
nslookup DC02.lab.local
```

```powershell
nltest /dsgetdc:lab.local /force
```

The domain controller discovery and connectivity checks completed successfully.

The secure channel was also verified:

```powershell
Test-ComputerSecureChannel -Verbose
```

The result was `True`.

### Resolution

After correcting the client's network configuration, domain authentication worked successfully.

The exact initial cause was not conclusively isolated, but the investigation identified an incorrect DHCP configuration as an important issue.

## 3. File Share Access Verification

### Problem / Test Objective

After configuring the HR and IT network shares, access was tested with two different domain users.

The objective was to ensure that users could access only their own department's share.

### Test Accounts

| User | Account | Department |
|---|---|---|
| Hans Wurst | `LAB\h.wurst` | HR |
| Max Mustermann | `LAB\m.mustermann` | IT |

### Tests and Results

| Test | Hans Wurst | Max Mustermann |
|---|---|---|
| Access `\\FILE01\HR` | Allowed | Denied |
| Access `\\FILE01\IT` | Denied | Allowed |
| Create file in own share | Successful | Successful |

### Resolution

The tests confirmed that the configured Active Directory group memberships, NTFS permissions and SMB share permissions enforce the intended department separation.

No additional permission changes were required after the successful tests.

## 4. Useful Troubleshooting Commands

The following commands were used during configuration and verification.

**Check network configuration:**

```powershell
ipconfig /all
```

**Check DNS resolution:**

```powershell
nslookup DC01.lab.local
```

**Check connectivity to a domain controller:**

```powershell
Test-NetConnection DC01 -Port 389
```

**Check domain controller discovery:**

```powershell
nltest /dsgetdc:lab.local /force
```

**Check the computer's secure channel:**

```powershell
Test-ComputerSecureChannel -Verbose
```

**Check SMB share permissions:**

```powershell
Get-SmbShareAccess -Name "HR","IT"
```

## 5. Screenshots

The following screenshots can be added as evidence:

- CLIENT02 network configuration after DHCP renewal
- Successful domain controller discovery
- Successful secure channel verification
- Successful HR and IT access tests
- Access denied when accessing the other department's share

<img width="744" height="480" alt="Screenshot 2026-11-25 161656" src="https://github.com/user-attachments/assets/68395ec5-f9f4-480f-9bcf-9e6dc1036020" />
<img width="769" height="603" alt="image" src="https://github.com/user-attachments/assets/09934cca-b968-4064-b4b1-68ac0b422f15" />

<img width="761" height="442" alt="Screenshot 2026-11-25 144203" src="https://github.com/user-attachments/assets/e3ffb26d-bc1f-4f58-8879-e6b1609d381e" />

<img width="780" height="332" alt="image" src="https://github.com/user-attachments/assets/4c5b8927-23db-4161-a881-af731c8a5ddd" />
<img width="767" height="396" alt="image" src="https://github.com/user-attachments/assets/3f1a0a8d-4c07-413a-b653-c2891c952045" />



## 6. Conclusion

The troubleshooting activities helped identify and resolve a domain login problem and verify the department-level access restrictions.

The tests confirmed that:

- CLIENT02 receives the expected network configuration.
- Domain controllers are reachable.
- DNS resolution for the domain works.
- The secure channel is healthy.
- HR and IT users can access their respective network shares.
- Access to the other department's share is denied.

These checks demonstrate practical troubleshooting skills in Windows Server, Active Directory, DNS, DHCP and file server administration.
