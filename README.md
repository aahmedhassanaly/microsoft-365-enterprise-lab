# Microsoft 365 Enterprise Lab

**Portfolio Priority: #5 — Microsoft 365 / Endpoint Administration**

A practical Microsoft 365 lab for **IT Infrastructure / Microsoft 365 Administration** using a small-company scenario.

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

## Architecture

<img src="Architecture/m365-enterprise-topology.svg" alt="Microsoft 365 enterprise topology" />

The lab connects on-premises Active Directory to Microsoft Entra ID and extends identity into Exchange Online, collaboration services, Intune, Conditional Access, and endpoint security.

## Tasks

| # | Task | Status |
|---:|---|:---:|
| 01 | [Tenant & Organization Setup](Documentation/01-tenant-organization-setup.md) | ✅ |
| 02 | [Entra ID Users & Groups](Documentation/02-entra-id-users-groups.md) | ✅ |
| 03 | [Entra ID Administration & Security](Documentation/03-entra-id-administration-security.md) | ✅ |
| 04 | [Exchange Online & Mailboxes](Documentation/04-exchange-online-mailboxes.md) | ✅ |
| 05 | [Exchange Mail Flow & Troubleshooting](Documentation/05-exchange-mail-flow-troubleshooting.md) | ✅ |
| 06 | [Microsoft Teams](Documentation/06-microsoft-teams.md) | ✅ |
| 07 | [SharePoint Online](Documentation/07-sharepoint-online.md) | ✅ |
| 08 | [OneDrive](Documentation/08-onedrive.md) | ✅ |
| 09 | [Intune Device Enrollment](Documentation/09-intune-device-enrollment.md) | ✅ |
| 10 | [Intune Configuration & Compliance](Documentation/10-intune-configuration-compliance.md) | ✅ |
| 11 | [Intune Application & Endpoint Management](Documentation/11-intune-application-endpoint-management.md) | ✅ |
| 12 | [Conditional Access](Documentation/12-conditional-access.md) | ✅ |
| 13 | [Microsoft Defender](Documentation/13-microsoft-defender.md) | ✅ |

Detailed implementation notes: [Documentation](Documentation/).

## Core Skills Demonstrated

### Identity
- Microsoft Entra ID
- Active Directory integration
- Cloud Sync
- Password Hash Synchronization
- Users and groups
- RBAC
- MFA
- Administrative Units

### Messaging
- Exchange Online mailboxes
- SMTP and aliases
- MX
- SPF, DKIM, DMARC
- Message Trace
- Mail-flow troubleshooting

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

## Troubleshooting Method

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

Examples include Cloud Sync scope problems, Exchange mail-flow issues, Intune application deployment, Conditional Access device identity, and Defender policy verification.

## PowerShell Scope

PowerShell was used for practical checks and administration where available.

Full Microsoft 365 PowerShell automation is **not completed** because the trial environment did not provide the required capability. This is intentionally not presented as a completed skill.

## Project Boundaries

This project does not claim advanced expertise in:

- Microsoft Graph automation
- SharePoint development / SPFx
- Microsoft Sentinel
- Advanced Defender for Cloud Apps
- Large migration projects
- Full Microsoft Purview implementation

## Result

**Identity → Messaging & Collaboration → Endpoint Management → Conditional Access → Endpoint Security**

The project demonstrates practical administration, verification, troubleshooting, and documentation rather than only configuration.
