# Active Directory – Group Policy Management

## 1. Overview

This section documents the centralized configuration of Windows settings using Group Policy Objects (GPOs) in the Active Directory domain `lab.local`.

Group Policy allows administrators to manage security settings and Windows configurations centrally across domain users and computers.

## 2. Group Policy Management

Group Policy is managed using the Group Policy Management Console (GPMC).

The console can be opened through:

**Server Manager → Tools → Group Policy Management**

GPMC allows administrators to:

- Create and edit Group Policy Objects.
- Link GPOs to domains and Organizational Units.
- Configure computer and user policies.
- Manage security settings centrally.
- Review GPO inheritance and policy application.

## 3. Planned Group Policy Configuration

The following policies are planned for this lab environment:

| Policy | Purpose | Scope |
|---|---|---|
| Password Policy | Define password requirements | Domain |
| Account Lockout Policy | Protect accounts against repeated failed logins | Domain |
| Desktop Restrictions | Manage selected Windows desktop settings | HR / IT |
| Windows Security Settings | Centralize selected security configurations | Domain or selected OUs |

## 4. Password and Account Lockout Policies

Password and account lockout settings are configured through the domain-level Group Policy.

The relevant policy path is:

**Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies**

The following settings can be configured:

- Password Policy
- Account Lockout Policy
- Password complexity requirements
- Minimum password length
- Account lockout threshold
- Account lockout duration

These settings help establish consistent security requirements for domain accounts.

## 5. Organizational Unit-Based Policies

Additional GPOs can be linked to specific Organizational Units.

For example:

| Organizational Unit | Possible GPO |
|---|---|
| HR | HR workstation restrictions |
| IT | IT workstation configuration |

This allows different settings to be applied to different departments.

## 6. Screenshots

The following screenshots will document the configuration:

- Group Policy Management Console
- Created Group Policy Objects
- Password Policy settings
- Account Lockout Policy settings
- GPO links to the relevant domain or Organizational Units
<img width="1052" height="397" alt="Screenshot 2026-11-26 090817" src="https://github.com/user-attachments/assets/c1904dca-da06-4caa-8783-968f4c92cbcd" />

## 7. Current Status

The Group Policy Management Console is used to manage centralized policies for the domain.

The planned policies will be configured and tested in the next steps.

## Next Step

Create and configure the selected Group Policy Objects and verify their application on CLIENT02.
