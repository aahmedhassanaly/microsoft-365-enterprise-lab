# Task 02 - Entra ID Users & Groups

## Objective

Integrate the existing on-premises Active Directory domain `kozika.local`
with Microsoft Entra ID using Microsoft Entra Cloud Sync.

The goal is to synchronize users and security groups from Active Directory
to Microsoft Entra ID and verify Password Hash Synchronization.

## Environment

- On-Premises Domain: `kozika.local`
- Microsoft 365 Domain: `kozika.online`
- Sync Method: Microsoft Entra Cloud Sync
- Password Hash Synchronization: Enabled
- Cloud Sync Scope: `OU=Microsoft365,DC=kozika,DC=local`

## Active Directory Users

| User | UPN |
|---|---|
| Ahmed Hassan | `ahmed.hassan@kozika.online` |
| Sara Ali | `sara.ali@kozika.online` |
| Mohamed Ahmed | `mohamed.ahmed@kozika.online` |
| Omar Khaled | `omar.khaled@kozika.online` |
| Nada Mohamed | `nada.mohamed@kozika.online` |

## Security Groups

- GG-IT
- GG-HR
- GG-Finance
- GG-Sales
- GG-Management

---

## 1. Configure the Active Directory UPN

The existing Active Directory domain uses the non-routable domain:

`kozika.local`

The verified Microsoft 365 domain is:

`kozika.online`

`kozika.online` was added as an Alternative UPN Suffix in Active Directory.

The five lab users were changed from:

`user@kozika.local`

to:

`user@kozika.online`

The Active Directory domain itself remained:

`kozika.local`.

---

## 2. Create a Microsoft 365 OU

The users were initially located in the default Active Directory `Users`
container.

A dedicated OU was created for Microsoft 365 synchronization:

    New-ADOrganizationalUnit -Name "Microsoft365" -Path "DC=kozika,DC=local"

The OU is:

    OU=Microsoft365,DC=kozika,DC=local

The five lab users were moved into this OU.

---

## 3. Move Users to the Microsoft365 OU

The following users were moved:

    $users = @(
        "ahmed.hassan",
        "sara.ali",
        "mohamed.ahmed",
        "omar.khaled",
        "nada.mohamed"
    )

    foreach ($user in $users) {
        Move-ADObject `
            -Identity (Get-ADUser -Identity $user).DistinguishedName `
            -TargetPath "OU=Microsoft365,DC=kozika,DC=local"
    }

The users were verified under:

    OU=Microsoft365,DC=kozika,DC=local

---

## 4. Install Microsoft Entra Provisioning Agent

The Microsoft Entra Provisioning Agent was installed on the Windows
Server used for the lab.

The agent was registered with Microsoft Entra ID.

A gMSA service account was created during the agent configuration.

The following services were verified as running:

    Microsoft Azure AD Connect Agent Updater
    Microsoft Azure AD Connect Provisioning Agent

The Cloud Sync agent status became:

    Active
<img width="1669" height="836" alt="image" src="https://github.com/user-attachments/assets/85d5cb10-eef6-4848-9d88-046293e58efe" />

---

## 5. Create Cloud Sync Configuration

A Microsoft Entra Cloud Sync configuration was created for:

    Domain: kozika.local
    Password Hash Sync: Enabled
    Device Sync: Disabled
    Exchange Hybrid Writeback: Disabled

The configuration status became:

    Healthy

---
<img width="1541" height="801" alt="image" src="https://github.com/user-attachments/assets/038e6f5c-f812-461a-9816-e234d95146d0" />

## 6. Configure Synchronization Scope

The Cloud Sync configuration was configured to synchronize the dedicated
Microsoft 365 OU:

    OU=Microsoft365,DC=kozika,DC=local

This OU contains the five lab users.

The dedicated OU was used because the default `Users` container was not
available for the required organizational-unit-based synchronization scope.

---

## 7. Provision Users to Microsoft Entra ID

The five Active Directory users appeared in Microsoft Entra ID as
synchronized users:

    ahmed.hassan@kozika.online
    sara.ali@kozika.online
    mohamed.ahmed@kozika.online
    omar.khaled@kozika.online
    nada.mohamed@kozika.online

The original cloud-only tenant administrator remained separate:

    ahmedhassan@kozika12.onmicrosoft.com
<img width="1919" height="852" alt="image" src="https://github.com/user-attachments/assets/9198e2f2-5b91-4cbf-be6b-d38ba1b3a805" />

---

## 8. Verify User Synchronization

A synchronized user was inspected in Microsoft Entra ID.

Example: Sara Ali

    UPN:
    sara.ali@kozika.online

    On-premises sync enabled:
    Yes

    On-premises domain:
    kozika.local

    On-premises SAM:
    sara.ali

    On-premises DN:
    CN=Sara Ali,OU=Microsoft365,DC=kozika,DC=local

This confirmed that the Microsoft Entra user was linked to the
on-premises Active Directory object.

---

## 9. Verify Group Synchronization

The following Active Directory security groups were synchronized:

    GG-Finance
    GG-HR
    GG-IT
    GG-Management
    GG-Sales

The groups appeared in Microsoft Entra ID with:

    Type:
    Security

    Source:
    Windows Server AD

-<img width="1919" height="887" alt="image" src="https://github.com/user-attachments/assets/876c3524-417a-4797-89d5-96bed134db85" />
--

## 10. Verify Group Membership Synchronization

Group membership was also verified.

### GG-Sales

The group contained:

    Omar Khaled

This matched the Active Directory membership.

### GG-IT

The group contained:

    Ahmed Hassan

This also matched the Active Directory membership.

This confirmed that both group objects and their memberships were
synchronized.

---

## 11. Password Hash Synchronization Test

Password Hash Synchronization was tested using Sara Ali.

The password state was checked in Active Directory:

    Get-ADUser -Identity "sara.ali" -Properties Enabled,PasswordLastSet,PasswordExpired,PasswordNeverExpires |
    Select-Object Name,Enabled,PasswordLastSet,PasswordExpired,PasswordNeverExpires

The account was initially found with an expired password.

A password reset was then performed:

    Set-ADAccountPassword -Identity "sara.ali" -Reset

The password state was verified again:

    Get-ADUser -Identity "sara.ali" -Properties PasswordLastSet,PasswordExpired |
    Select-Object Name,PasswordLastSet,PasswordExpired

The result showed:

    PasswordLastSet  : <new timestamp>
    PasswordExpired  : False

After the synchronization period, Sara successfully signed in to
Microsoft 365 using the new password.

This provided a practical test of the password synchronization flow:

    Active Directory
            |
            v
    Password Hash Synchronization
            |
            v
    Microsoft Entra ID
            |
            v
    Microsoft 365 Authentication

The test password is not documented.
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/a89a86f5-d2a6-4a6d-be88-670d8ddd0702" />

---

## 12. Troubleshooting

### Problem

The Cloud Sync configuration initially showed no results when selecting
organizational units.

### Investigation

The users were checked using PowerShell:

    Get-ADUser -Filter * |
    Where-Object {$_.SamAccountName -in @(
        "ahmed.hassan",
        "sara.ali",
        "mohamed.ahmed",
        "omar.khaled",
        "nada.mohamed"
    )} |
    Select-Object Name,DistinguishedName

The users were initially located under:

    CN=Users,DC=kozika,DC=local

This was the default Active Directory `Users` container.

### Fix

A dedicated OU was created:

    OU=Microsoft365,DC=kozika,DC=local

The five users were moved to the new OU.

The new OU was then selected as the Cloud Sync synchronization scope.

### Verification

Cloud Sync successfully synchronized the users after the scope was
corrected.

---

## 13. Final Verification

| Component | Status |
|---|---|
| Entra ID Users | Completed |
| AD Users | Completed |
| Custom UPN `@kozika.online` | Completed |
| Microsoft365 OU | Completed |
| Cloud Sync Agent | Completed |
| Cloud Sync Configuration | Completed |
| User Synchronization | Completed |
| Group Synchronization | Completed |
| Group Membership Synchronization | Completed |
| Password Hash Synchronization | Tested Successfully |
| Password Change Test | Successful |

---

## Result

Task 02 is complete.

The existing Kozika environment now has hybrid identity synchronization
between the on-premises Active Directory environment and Microsoft Entra ID.

The final architecture is:

    Active Directory
    kozika.local
            |
            v
    Microsoft Entra Cloud Sync
            |
            v
    Microsoft Entra ID
            |
            v
    Microsoft 365

Users and security groups are synchronized from the existing Active
Directory environment.

Password Hash Synchronization was also tested successfully by changing
a user's password in Active Directory and signing in to Microsoft 365
using the new password.

---

## Key Skills Practiced

- Microsoft Entra ID user management
- Microsoft Entra ID groups
- Active Directory UPN management
- Alternative UPN Suffixes
- Microsoft Entra Cloud Sync
- Provisioning Agent
- Password Hash Synchronization
- AD-to-Entra user synchronization
- AD-to-Entra group synchronization
- Group membership synchronization
- OU-based synchronization scope
- Hybrid identity troubleshooting
- PowerShell Active Directory commands

## Task Status

**COMPLETED**
