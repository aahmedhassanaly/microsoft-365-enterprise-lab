# Microsoft 365 Enterprise Lab

A practical Microsoft 365 lab for **IT Infrastructure / Microsoft 365 Administration**.

The lab uses a small company called **Kozika Online** and covers identity, email, collaboration, device management, and security.

## Environment

- Microsoft 365
- Microsoft Entra ID
- Windows Server / Active Directory
- Microsoft Entra Cloud Sync
- Exchange Online
- Microsoft Teams
- SharePoint Online
- OneDrive
- Microsoft Intune
- Conditional Access
- Microsoft Defender

### Architecture

```text
Active Directory
     │
     │ Cloud Sync + PHS
     ▼
Microsoft Entra ID
     │
     ├── Exchange Online
     ├── Teams
     ├── SharePoint
     ├── OneDrive
     └── Intune
             │
             ▼
        Windows 11
             │
       Conditional Access
             │
          Defender
```

[View the topology diagram](Architecture/m365-enterprise-topology.svg)

## Lab Tasks

| # | Task | Status |
|---|---|---|
| 01 | Tenant & Organization Setup | ✅ |
| 02 | Entra ID Users & Groups | ✅ |
| 03 | Entra ID Administration & Security | ✅ |
| 04 | Exchange Online & Mailboxes | ✅ |
| 05 | Exchange Mail Flow & Troubleshooting | ✅ |
| 06 | Microsoft Teams | ✅ |
| 07 | SharePoint Online | ✅ |
| 08 | OneDrive | ✅ |
| 09 | Intune Device Enrollment | ✅ |
| 10 | Intune Configuration & Compliance | ✅ |
| 11 | Intune Application Management | ✅ |
| 12 | Conditional Access | ✅ |
| 13 | Microsoft Defender | ✅ |

See the full tasks in the [Documentation](Documentation/).

## Main Skills

### Identity
- Microsoft Entra ID
- Active Directory integration
- Cloud Sync
- Password Hash Synchronization
- Users and groups
- RBAC
- MFA
- Administrative Units

### Exchange Online
- Mailbox management
- SMTP and aliases
- MX
- SPF, DKIM, DMARC
- Message Trace
- Mail flow troubleshooting

### Endpoint Management
- Intune enrollment
- Configuration profiles
- Compliance policies
- Win32 applications
- Application troubleshooting
- Endpoint verification

### Security
- Conditional Access
- MFA
- Device compliance
- Sign-in logs
- Microsoft Defender
- Endpoint security

## Troubleshooting

The lab uses this method:

```text
Problem
   ↓
Evidence
   ↓
Hypothesis
   ↓
Test
   ↓
Fix
   ↓
Verify
   ↓
Document
```

Examples include:

- Cloud Sync scope problem
- Exchange mail flow problem
- Intune application deployment problem
- Conditional Access device problem
- Defender policy verification

The goal is not only to configure a service, but also to **find problems and verify the fix**.

## PowerShell

PowerShell was used for practical checks and administration where available.

Full Microsoft 365 PowerShell automation is **not completed** in this lab because the trial environment did not provide the required capability.

This is intentionally not presented as a completed skill.

## Project Scope

This project focuses on Microsoft 365 administration and IT Infrastructure.

It does not claim advanced skills in:

- Microsoft Graph automation
- SharePoint development
- SPFx
- Microsoft Sentinel
- Advanced Defender for Cloud Apps
- Large migration projects
- Full Microsoft Purview implementation

## Project Status

**13 practical tasks completed.**

The main goal is:

**Understand → Configure → Verify → Troubleshoot → Explain → Document**

**Career focus:** IT Infrastructure / Microsoft 365 / Endpoint Administration / Junior System Administration
