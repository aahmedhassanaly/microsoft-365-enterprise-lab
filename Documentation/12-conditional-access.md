# Task 12 — Conditional Access

## Objective

Configure and test Microsoft Entra Conditional Access policies to control access to Microsoft 365 resources based on user identity, MFA, and device compliance.

The lab focuses on:

- Conditional Access policies
- MFA enforcement
- Device compliance
- Report-only mode
- What If simulation
- Sign-in Logs
- Conditional Access troubleshooting

---

## Business Scenario

Kozika IT wants to improve Microsoft 365 access security.

The security requirements are:

1. Ahmed must use MFA when accessing Exchange Online.
2. Ahmed must use a compliant device when accessing Exchange Online.
3. Policies should be tested before enforcement.
4. Administrators must be able to troubleshoot access problems using Microsoft Entra sign-in logs.

---

## Environment

### Microsoft 365

- Tenant: `kozika.online`
- User: `ahmed.hassan@kozika.online`
- Platform: Microsoft Entra ID
- Device Management: Microsoft Intune
- Device: `DESKTOP-2J1L8D5`

### Device Status

The Windows device is:

- Microsoft Entra Registered
- Intune managed
- Compliant

The device is not Microsoft Entra Joined.

---

# 1. Conditional Access Overview

Conditional Access uses an **If → Then** logic.

Example:

> If Ahmed accesses Exchange Online → require MFA.

Another example:

> If Ahmed accesses Exchange Online → require a compliant device.

A Conditional Access policy can use:

- Users and groups
- Cloud applications
- Device platforms
- Locations
- Client applications
- Device state

The policy can then apply controls such as:

- Require MFA
- Require a compliant device
- Block access

---

# 2. MFA Conditional Access Policy

Created policy:

`CA-Require-MFA-Ahmed`

### Users

Selected Ahmed:

`ahmed.hassan@kozika.online`

The tenant also contained the original cloud administrator account:

`ahmedhassan@kozika12.onmicrosoft.com`

This account was also included during the lab test.

### Target Resource

Selected:

`Office 365 Exchange Online`

### Grant

Configured:

`Require multifactor authentication`

### Initial State

The policy was first tested using:

`Report-only`

After successful testing, the policy was changed to:

`On`

---

# <img width="1594" height="805" alt="image" src="https://github.com/user-attachments/assets/35359e55-b9d0-4d7e-bdf7-cd133a3d1f70" />
3. Testing MFA

The policy was tested using a real Microsoft 365 sign-in.

The user accessed:

`Office 365 Exchange Online`

The Conditional Access result showed:

`CA-Require-MFA-Ahmed → Mfa → Success`

After the policy was changed to **On**, the user was required to complete MFA.

This confirmed that the policy was enforcing MFA successfully.

---

# 4. What If Tool

The Conditional Access **What If** tool was used to simulate policy evaluation.

Example test:

- User: Ahmed
- Cloud app: Exchange Online
- Device platform: Windows
- Client app: Browser

The What If tool showed whether Conditional Access policies would apply to the selected conditions.

### Important

What If is a simulation.

It does not replace a real sign-in test.

For real troubleshooting, use:

`Microsoft Entra ID → Monitoring → Sign-in logs`

---

# 5. Compliant Device Policy

Created policy:

`CA-Require-Compliant-Device-Ahmed`

### User

`ahmed.hassan@kozika.online`

### Target Resource

`Office 365 Exchange Online`

### Grant

Configured:

`Require device to be marked as compliant`

### Initial State

The policy was first configured as:

`Report-only`

After testing, it was changed to:

`On`

---
<img width="1073" height="776" alt="image" src="https://github.com/user-attachments/assets/08461fb0-ac2a-429a-8e1e-92787c0c0631" />

# 6. Device Identification Test

The device was tested using different browsers.

## Chrome

The sign-in information showed:

- Device ID: Empty
- Managed: No
- Compliant: No
- Join Type: Empty

Because the device information was not available in the sign-in context, the compliant-device requirement could not recognize the device correctly.

The browser eventually displayed:

`You can't get there from here`

This was consistent with the Conditional Access requirement for a managed/compliant device.

---

## Microsoft Edge

The same device was tested using Edge.

The sign-in information showed:

- Device ID: `19cfbfe0-460a-46c8-8e1d-e253d6a961b1`
- Managed: Yes
- Compliant: Yes
- Join Type: Azure AD registered
- Client App: Browser
- Application: One Outlook Web
- Resource: Office 365 Exchange Online
- Status: Success

Edge successfully provided the device identity information required by Conditional Access.

---

# 7. Device Registration Verification

The following command was used:

    dsregcmd /status

Important results:

    AzureAdJoined : NO
    EnterpriseJoined : NO
    DomainJoined : NO
    WorkplaceJoined : YES

The device was therefore:

- Microsoft Entra Registered
- Not Microsoft Entra Joined
- Not domain joined
- Managed by Intune

The Work Account section showed:

    WorkplaceTenantName : kozika
    WorkplaceMdmUrl : https://enrollment.manage.microsoft.com/enrollmentserver/discovery.svc

The device ID was:

    19cfbfe0-460a-46c8-8e1d-e253d6a961b1

---

# 8. Real Sign-in Verification

After enabling the Conditional Access policies, the sign-in logs were checked.

The final results included:

| Policy | Control | Result |
|---|---|---|
| CA-Require-MFA-Ahmed | Mfa | Success |
| CA-Require-Compliant-Device-Ahmed | RequireCompliantDevice | Success |
| Require multifactor authentication for all users | Mfa | Success |
| Require multifactor authentication for admins | Mfa | Not applied |
| Block legacy authentication | Block | Not applied |
| Require multifactor authentication for Azure management | Mfa | Not applied |

The Microsoft-managed policies already existed in the tenant and were not created as part of this lab.
<img width="1906" height="843" alt="image" src="https://github.com/user-attachments/assets/ec9169fe-99c7-48a8-a140-b60f523dcfe0" />

---

# 9. Troubleshooting Method

The Conditional Access troubleshooting process used in this lab was:

### Problem

Access behavior was different between Chrome and Edge.

### Evidence

Chrome did not provide device identity:

- Managed: No
- Compliant: No
- Device ID: Empty

Edge provided the device identity:

- Managed: Yes
- Compliant: Yes
- Device ID available

### Hypothesis

The browser sign-in context was affecting how the device was identified by Conditional Access.

### Test

The same user and device were tested with both browsers.

### Result

Edge successfully passed the Conditional Access requirements.

Chrome was blocked by the compliant-device requirement.
<img width="1919" height="848" alt="image" src="https://github.com/user-attachments/assets/c3e30a30-522c-4be4-a374-13142c2f8549" />

### Verification

Microsoft Entra Sign-in Logs confirmed:

`CA-Require-MFA-Ahmed → Success`

`CA-Require-Compliant-Device-Ahmed → Success`

---

# 10. Important Concepts Learned

## Report-only

Report-only evaluates the policy without enforcing the access control.

It is useful before enabling a new Conditional Access policy.

## What If

What If simulates which Conditional Access policies may apply to specific conditions.

It is useful for testing policy logic.

## Sign-in Logs

Sign-in Logs show what actually happened during a real authentication attempt.

They are more important than What If when troubleshooting real access problems.

## Conditional Access

Conditional Access controls access based on conditions.

Example:

    If user = Ahmed
    AND application = Exchange Online
    THEN require MFA

Another example:

    If user = Ahmed
    AND application = Exchange Online
    THEN require compliant device

---

# 11. Final Verification

The following requirements were successfully tested:

- Conditional Access policy created.
- MFA requirement configured.
- MFA policy tested in Report-only mode.
- MFA policy enabled.
- Real MFA challenge successfully completed.
- Compliant-device policy created.
- Compliant-device policy tested.
- Device compliance recognized through Edge.
- Chrome behavior investigated.
- What If used for policy simulation.
- Sign-in Logs used for real verification.
- Conditional Access results showed Success.

---

# Skills Practiced

- Microsoft Entra Conditional Access
- MFA enforcement
- Device compliance access control
- Report-only policies
- What If
- Microsoft Entra Sign-in Logs
- Device identity troubleshooting
- Browser/device authentication troubleshooting
- Conditional Access verification

---

# Task Result

**COMPLETED**

The lab demonstrated how Conditional Access can enforce MFA and device compliance requirements for Microsoft 365 access and how to troubleshoot the result using device information and sign-in logs.
