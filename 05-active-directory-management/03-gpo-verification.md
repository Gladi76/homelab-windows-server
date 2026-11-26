# Active Directory – GPO Verification

## 1. Overview

This section documents the verification of Group Policy Objects (GPOs) in the Active Directory domain `lab.local`.

The objective is to confirm that configured Group Policies are correctly applied to domain users and computers.

## 2. Test Environment

| Component | Configuration |
|---|---|
| Domain | `lab.local` |
| Domain Controller | DC01 |
| Client Computer | CLIENT02 |
| Client IP Address | 192.168.178.240 |
| Operating System | Windows 11 |
| Group Policy Management | Group Policy Management Console |

## 3. Group Policy Update

After configuring or changing a Group Policy, the client can request an updated policy using:

```cmd
gpupdate /force
```

This command forces the computer and user policy settings to be refreshed.

A restart or user sign-out may be required for certain policy settings to take effect.

## 4. Group Policy Verification

The following command displays the applied Group Policy information:

```cmd
gpresult /r
```

The output provides information about:

- Applied Group Policy Objects
- User policy settings
- Computer policy settings
- Domain and organizational unit information

A detailed HTML report can be generated using:

```cmd
gpresult /h C:\Temp\gpo-report.html
```

The generated report can be opened in a web browser.

## 5. Verification Checklist

The following checks will be performed on CLIENT02:

- [ ] Domain connectivity is available.
- [ ] Group Policy update completes successfully.
- [ ] Expected GPOs appear in the applied policy list.
- [ ] Computer policies are applied.
- [ ] User policies are applied where configured.
- [ ] Configured security settings are effective.

## 6. Screenshots

The following screenshots will be added:

- Successful execution of `gpupdate /force`
- Applied Group Policy Objects from `gpresult /r`
- Detailed Group Policy HTML report
- Verification of selected policy settings
<img width="943" height="492" alt="image" src="https://github.com/user-attachments/assets/41edfa60-d0fe-42cd-b4b6-ffecc4b0e014" />

<img width="942" height="524" alt="image" src="https://github.com/user-attachments/assets/0eca5e87-b5ad-41ed-83dd-9cb4ecb63997" />

## 7. Result

The Group Policy configuration will be considered verified after the expected policies have been successfully applied to CLIENT02.

The verification results and any troubleshooting activities will be documented here.

## Conclusion

Group Policy verification confirms that centralized Active Directory policies are reaching the intended domain users and computers.

This demonstrates practical experience with Group Policy management, client policy updates and troubleshooting in a Windows Server environment.
