# FILE01 – Verification and Access Testing

## 1. Overview

This section documents the verification of the FILE01 file server configuration.

Practical access tests were performed using two domain user accounts to verify department-level access restrictions.

## 2. Test Environment

| Component | Configuration |
|---|---|
| File Server | FILE01 |
| IP Address | 192.168.178.236 |
| Domain | `lab.local` |
| Client | CLIENT02 |
| HR Share | `\\FILE01\HR` |
| IT Share | `\\FILE01\IT` |

## 3. User Accounts

The following domain accounts were used for testing:

| User | Account | Department |
|---|---|---|
| Hans Wurst | `LAB\h.wurst` | HR |
| Max Mustermann | `LAB\m.mustermann` | IT |

## 4. Access Tests

The following tests were performed from CLIENT02 using the respective domain accounts.

| Test | Hans Wurst (HR) | Max Mustermann (IT) |
|---|---|---|
| Access HR share | Allowed | Denied |
| Access IT share | Denied | Allowed |
| Create test file in own department share | Successful | Successful |

Both users could access and create files in their own department shares.

Access to the other department's share was denied as expected.

## 5. Verification Results

The practical tests confirmed the following:

- Hans Wurst can access the HR share.
- Hans Wurst cannot access the IT share.
- Max Mustermann can access the IT share.
- Max Mustermann cannot access the HR share.
- Both users can create files in their respective department shares.

## 6. Screenshots

### HR Access – Hans Wurst

The screenshot shows Hans Wurst accessing the HR network share and creating a test file.

### IT Access – Max Mustermann

The screenshot shows Max Mustermann accessing the IT network share and creating a test file.

### Access Denied – Department Separation

The screenshots show that each user is denied access to the other department's network share.

## 7. Final Result

The FILE01 file server was successfully configured and tested.

- File Server role installed.
- Separate data disk configured.
- HR and IT folder structure created.
- NTFS permissions assigned through Active Directory security groups.
- SMB shares configured with restricted access.
- Department-level access successfully tested.
- Read and write access verified for both department users.

The file server is operational and provides separate network storage for the HR and IT departments.

## Conclusion

The practical tests confirmed that Active Directory security groups, NTFS permissions and SMB share permissions work together to enforce department-level access restrictions.
