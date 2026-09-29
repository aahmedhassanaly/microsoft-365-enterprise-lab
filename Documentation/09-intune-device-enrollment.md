# Task 09 — Intune Device Enrollment

## Objective

The goal of this task was to enroll a Windows device into Microsoft Intune and verify that the device became managed.

The lab also included a real enrollment troubleshooting scenario.

## Environment

- Microsoft 365 Tenant: `kozika.online`
- Microsoft Intune
- Windows device: `DESKTOP-2J1L8D5`
- Primary user: Ahmed Hassan
- Device ownership: Personal
- Management: Intune

## 1. Automatic Enrollment

Opened:

Microsoft Intune admin center → Devices → Enrollment → Automatic Enrollment

### MDM User Scope

Configured:

- MDM user scope: Some
- Ahmed Hassan included in the scope

This allows the selected user to use automatic MDM enrollment.

The default MDM URLs were kept unchanged.
<img width="1919" height="872" alt="image" src="https://github.com/user-attachments/assets/875646f5-e0e2-4ccc-b03c-7eefcc9040b0" />

### WIP

Windows Information Protection was not configured for this lab.

- WIP user scope: None

## 2. Device Platform Restrictions

Opened:

Devices → Enrollment → Device platform restrictions

Reviewed the default restriction.

Current configuration:

- Applies to: All Users
- Windows (MDM): Allow
- Windows minimum version: Allow
- Windows maximum version: Allow

No changes were required because Windows enrollment was already allowed.

## 3. Device Limit Restriction

Reviewed:

Devices → Enrollment → Device limit restriction

Current configuration:

- Applies to: All Users
- Device limit: 5

The default value was kept because it was sufficient for the lab.

## 4. Initial Enrollment Test

The Windows device was connected through:

Settings → Accounts → Access work or school → Connect

The Microsoft 365 account used for the test was:

`ahmed.hassan@kozika.online`

The first enrollment attempt produced an error:

`0x80180018`

The tenant and licensing configuration were then checked.

## 5. Licensing and Tenant Verification

The Ahmed Hassan license showed:

- Microsoft 365 Business Premium with Copilot
- Microsoft Intune: Enabled
- Microsoft Intune Plan 1: Enabled
- Microsoft Entra ID P1: Enabled

Tenant status was also checked.

Results:

- MDM Authority: Microsoft Intune
- Account status: Active
- Total licensed users: 1
- Total Intune licenses: 1
- Total enrolled devices: 0 at that time

The Intune tenant configuration was therefore valid.

## 6. Enrollment Troubleshooting

The Windows MDM diagnostic log was checked:

Microsoft → Windows → DeviceManagement-Enterprise-Diagnostics-Provider → Admin

An Event ID 4223 was found.

The event showed:

- ErrorType: Authentication
- Message: Authentication

This confirmed that the enrollment request reached the device enrollment service but the authentication process failed.

The next diagnostic check used:

`dsregcmd /status`

The device initially showed:

- AzureAdJoined: NO
- DomainJoined: NO
- WorkplaceJoined: YES
- AzureAdPrt: NO

The existing Workplace registration belonged to another organization:

`Alexandria University`

The old Work/School connection was removed from the device.

After restarting the computer, `dsregcmd /status` showed:

- AzureAdJoined: NO
- DomainJoined: NO
- WorkplaceJoined: NO
- AzureAdPrt: NO

The old workplace registration was therefore removed successfully.

## 7. Successful Enrollment

The Windows device was enrolled again using:

Settings → Accounts → Access work or school → Connect

The enrollment completed successfully.

Windows displayed:

"Setting up your device"

The device then showed:

- Areas managed by kozika
- Management Server Address
- Device sync information
- Sync option

This confirmed that the device had been enrolled into MDM.

## 8. Intune Verification

Opened:

Microsoft Intune admin center → Devices → Windows → Windows devices

The device appeared as:

- Device: `DESKTOP-2J1L8D5`
- Model: Precision 5520
- Manufacturer: Dell Inc.
- OS: Windows
- Ownership: Personal
- Management: Intune
- Primary user: Ahmed Hassan
- Status: Compliant
- Last check-in: 09/29/2026
- Management name: `ahmed.hassan_Windows_9/29/2026_10:37 AM`

The device successfully checked in with Intune.
<img width="1635" height="830" alt="image" src="https://github.com/user-attachments/assets/f68ae125-fdde-415b-8625-6f638fe7933a" />

## 9. Final Configuration

| Setting | Result |
|---|---|
| MDM User Scope | Some |
| Windows MDM | Allowed |
| Device Limit | 5 |
| WIP | None |
| Intune MDM Authority | Microsoft Intune |
| Device Enrollment | Successful |
| Device Ownership | Personal |
| Device Management | Intune |
| Device Check-in | Successful |

## Troubleshooting Method

The main troubleshooting process was:

Problem → Evidence → Hypothesis → Test → Fix → Verify

### Problem

Windows enrollment failed with `0x80180018`.

### Evidence

- Intune license was enabled.
- Intune was the MDM authority.
- Event ID 4223 showed Authentication.
- `dsregcmd /status` showed an existing Workplace registration.

### Fix

The old Workplace registration belonging to Alexandria University was disconnected.

### Verification

The device was enrolled again and appeared successfully in Intune with an active check-in.

## Key Skills

After this task, the lab covered:

- Windows MDM enrollment
- Automatic Enrollment
- MDM User Scope
- Device Platform Restrictions
- Device Limit Restrictions
- Work or School enrollment
- Intune device verification
- `dsregcmd /status`
- Windows MDM diagnostic logs
- Enrollment troubleshooting
- Device check-in

## Task Result

**COMPLETED**

The Windows device is successfully enrolled and managed by Microsoft Intune.
