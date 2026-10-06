# Microsoft 365 Enterprise Lab

A hands-on Microsoft 365 administration lab built around a fictional organization, **Kozika Online**.

The lab is designed to demonstrate practical administration, configuration, verification, and troubleshooting across Microsoft Entra ID, Exchange Online, Teams, SharePoint, OneDrive, Microsoft Intune, Conditional Access, and Microsoft Defender.

> **Career focus:** This repository is intentionally built around real administrator workflows and troubleshooting evidence rather than a collection of isolated portal screenshots.

---

## Project Overview

**Organization:** Kozika Online  
**Microsoft 365 tenant:** `kozika12.onmicrosoft.com`  
**Custom domain:** `kozika.online`  
**On-premises AD domain:** `kozika.local`  
**Identity synchronization:** Microsoft Entra Cloud Sync + Password Hash Synchronization  
**Endpoint management:** Microsoft Intune  
**Endpoint security:** Microsoft Defender for Endpoint / Microsoft Defender Antivirus

The environment combines an on-premises Windows Server / Active Directory environment with Microsoft 365 cloud services.

### High-level architecture

**On-Premises**

`Active Directory (kozika.local)`  
→ Users / Groups / UPN  
→ Microsoft Entra Cloud Sync  
→ **Microsoft Entra ID**

**Microsoft 365**

Entra ID  
→ Exchange Online  
→ Teams  
→ SharePoint Online  
→ OneDrive for Business  
→ Intune  
→ Conditional Access  
→ Microsoft Defender

**Managed Windows endpoint**

Windows 11  
→ Entra registered  
→ Intune managed  
→ Compliance evaluated  
→ Defender protected  
→ Conditional Access evaluated during Microsoft 365 access

---

## Architecture Diagram

![Microsoft 365 Enterprise Lab Topology](Architecture/m365-enterprise-topology.svg)

The topology source is stored in **[`Architecture/`](Architecture/)**.

- Renderable diagram: `Architecture/m365-enterprise-topology.svg`

The diagram shows the relationship between the on-premises AD environment, Entra ID, Microsoft 365 workloads, Intune, Defender, Conditional Access, and the managed Windows endpoint.

---

## Lab Objectives

This lab was built to practice the lifecycle an IT / Microsoft 365 administrator would actually work with:

**Understand → Configure → Verify → Troubleshoot → Explain → Document**

Key objectives:

- Build and configure a Microsoft 365 tenant.
- Connect a custom domain and manage DNS dependencies.
- Synchronize identities from on-premises Active Directory.
- Apply least privilege with Entra ID administrative roles.
- Configure and test MFA.
- Use Administrative Units for scoped administration.
- Administer Exchange Online mailboxes and mail flow.
- Troubleshoot mail delivery using evidence and Message Trace.
- Configure basic Teams collaboration.
- Manage SharePoint sites, libraries, permissions, and sharing.
- Configure OneDrive administration and synchronization settings.
- Enroll and manage Windows devices with Intune.
- Configure compliance and endpoint security policies.
- Deploy and troubleshoot Win32 applications.
- Use Conditional Access to enforce MFA and device compliance.
- Onboard and manage Windows endpoints with Microsoft Defender.
- Verify cloud policies against actual endpoint state.

---

# Tasks

| # | Task | Main Skills | Status |
|---|---|---|---|
| 01 | [Tenant & Organization Setup](Documentation/01-tenant-organization-setup.md) | Tenant, custom domain, DNS, organization setup | ✅ Completed |
| 02 | [Entra ID Users & Groups](Documentation/02-entra-id-users-groups.md) | AD, UPN, Cloud Sync, PHS, users, groups | ✅ Completed |
| 03 | [Entra ID Administration & Security](Documentation/03-entra-id-administration-security.md) | RBAC, least privilege, MFA, Administrative Units | ✅ Completed |
| 04 | [Exchange Online & Mailboxes](Documentation/04-exchange-online-mailboxes.md) | Mailboxes, SMTP, aliases, forwarding, restrictions | ✅ Completed |
| 05 | [Exchange Mail Flow & Troubleshooting](Documentation/05-exchange-mail-flow-troubleshooting.md) | SPF, DKIM, DMARC, Message Trace, mail flow rules | ✅ Completed |
| 06 | [Microsoft Teams](Documentation/06-microsoft-teams.md) | Teams, channels, roles, private channels, policies | ✅ Completed |
| 07 | [SharePoint Online](Documentation/07-sharepoint-online.md) | Sites, libraries, permissions, sharing, version history | ✅ Completed |
| 08 | [OneDrive for Business](Documentation/08-onedrive.md) | Admin settings, retention, sync, file restrictions | ✅ Completed |
| 09 | [Intune Device Enrollment](Documentation/09-intune-device-enrollment.md) | MDM, enrollment, restrictions, troubleshooting | ✅ Completed |
| 10 | [Intune Configuration & Compliance](Documentation/10-intune-configuration-compliance.md) | Configuration profiles, compliance, monitoring | ✅ Completed |
| 11 | [Intune Application & Endpoint Management](Documentation/11-intune-application-endpoint-management.md) | Win32 apps, detection, IME, logs, uninstall | ✅ Completed |
| 12 | [Conditional Access](Documentation/12-conditional-access.md) | MFA, compliant devices, What If, sign-in troubleshooting | ✅ Completed |
| 13 | [Microsoft Defender](Documentation/13-microsoft-defender.md) | Defender onboarding, AV policy, endpoint verification | ✅ Completed |

---

## What This Lab Demonstrates

### Identity & Access

- Microsoft Entra ID administration
- On-premises Active Directory integration
- Alternative UPN suffixes
- Microsoft Entra Cloud Sync
- Password Hash Synchronization
- User and security group synchronization
- Role-Based Access Control
- Least privilege
- Administrative Units
- Microsoft Authenticator
- MFA verification

### Exchange Online

- Mailbox administration
- Primary and secondary SMTP addresses
- Mailbox settings
- Forwarding
- Delivery restrictions
- MX configuration
- SPF
- DKIM
- DMARC
- Message Trace
- Mail flow rules
- Mail delivery troubleshooting

### Collaboration

- Microsoft Teams
- Team roles
- Standard and private channels
- Teams policies
- SharePoint team sites
- Document libraries
- SharePoint permissions
- Sharing controls
- Version history
- OneDrive administration
- OneDrive synchronization controls

### Endpoint Management

- Intune automatic enrollment
- MDM user scope
- Device platform restrictions
- Device limits
- Configuration profiles
- Firewall configuration
- Compliance policies
- Noncompliance actions
- Win32 application packaging
- Detection rules
- Application assignments
- Microsoft Intune Management Extension
- IME log analysis
- Application uninstall
- Endpoint verification

### Security

- Conditional Access
- Report-only mode
- MFA enforcement
- Compliant-device access control
- What If simulation
- Sign-in log analysis
- Device identity troubleshooting
- Microsoft Defender for Endpoint onboarding
- Microsoft Defender Antivirus policies
- Endpoint security verification

---

# Troubleshooting Approach

A major purpose of this lab is to demonstrate **engineering troubleshooting**, not just configuration.

The recurring methodology is:

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

Examples demonstrated in the lab include:

### Hybrid Identity

Cloud Sync initially could not use the expected synchronization scope.

**Evidence:** Users were located in the default `Users` container.  
**Fix:** Created `OU=Microsoft365` and moved the users into it.  
**Verification:** Cloud Sync successfully provisioned the users.

### Entra Scoped Administration

A scoped User Administrator could not reset a user outside the assigned Administrative Unit.

**Evidence:** Permission boundary prevented the operation.  
**Result:** Confirmed that the AU scope was actually being enforced.

### Exchange Mail Flow

A mail delivery issue was investigated using Message Trace and message events instead of assuming that a pending state represented a permanent failure.

### Intune Applications

Application deployment was investigated using:

- Intune assignment status
- Device state
- Intune Management Extension
- `AppWorkload.log`
- Local PowerShell / file detection

This demonstrated the difference between **portal reporting** and **actual endpoint state**.

### Conditional Access

The same Windows device behaved differently between Chrome and Edge.

Evidence from the sign-in context and `dsregcmd /status` was used to understand device identity and why the compliant-device requirement behaved differently.

### Defender

Centralized policy deployment was verified at multiple layers:

**Intune policy → device check-in → PowerShell → Windows Security**

---

# Verification Philosophy

A key principle throughout the project is:

> **Never rely on a portal status alone when troubleshooting.**

Where possible, the lab verifies the final state from more than one layer.

Examples:

| Area | Cloud Evidence | Endpoint / Independent Evidence |
|---|---|---|
| Cloud Sync | Entra user state | AD object / synchronization configuration |
| Password Hash Sync | Microsoft 365 sign-in | AD password change |
| Intune enrollment | Intune device status | Windows device state |
| Win32 apps | Intune deployment status | Installed files + IME logs |
| Compliance | Intune compliance state | Endpoint configuration |
| Defender | Intune policy/check-in | `Get-MpComputerStatus` + Windows Security |
| Conditional Access | Sign-in Logs | `dsregcmd /status` + browser/device behavior |

---

# Practical Evidence

The repository contains screenshots and documented verification steps throughout the tasks.

Evidence includes:

- Tenant and domain configuration
- Cloud Sync agent and configuration
- Synchronized users and groups
- MFA registration and testing
- Administrative Unit scoping
- Exchange configuration
- Mail flow and Message Trace
- Teams configuration
- SharePoint permissions
- Intune enrollment
- Configuration and compliance status
- Win32 application deployment
- IME logs
- Conditional Access results
- Device registration state
- Defender onboarding
- Endpoint security verification

---

# PowerShell Scope

PowerShell is used in the lab where it provides practical verification or administration evidence, including:

- Active Directory user and OU operations
- Password state verification
- Device verification
- Defender status verification
- Application detection

Full Microsoft 365 PowerShell automation is **not claimed as completed in this repository**.

The current Microsoft 365 trial environment did not provide the required PowerShell capability for the planned automation work, so the project intentionally does not add artificial automation tasks just to increase the task count.

Future automation topics can be practiced in a separate suitable environment:

- Bulk user onboarding
- Group management
- Licensing
- Exchange reporting
- Offboarding
- Administrative reporting

---

# Project Boundaries

This repository focuses on **Microsoft 365 administration and endpoint/infrastructure operations**.

It is intentionally not a development project.

The following areas are therefore not presented as completed skills:

- Advanced Microsoft Graph automation
- SharePoint development
- SPFx
- Advanced Power Automate development
- Microsoft Sentinel
- Advanced Defender for Cloud Apps
- Large-scale migration projects
- Full Microsoft Purview implementation

These can be added later only when they provide meaningful value for the target role.

---

# Security & Lab Notes

- The organization and domains are used for training purposes.
- No passwords or authentication secrets are documented.
- Test credentials should never be committed to GitHub.
- Screenshots should be reviewed before publishing to ensure that secrets, tokens, recovery information, or personal data are not exposed.
- The environment was intentionally built as a disposable training environment.

---

# Current Project Assessment

The lab currently demonstrates a broad Microsoft 365 administration foundation across:

**Identity → Messaging → Collaboration → Endpoint Management → Conditional Access → Endpoint Security**

The strongest evidence is in the areas of:

- Hybrid identity troubleshooting
- Exchange mail-flow troubleshooting
- Intune deployment and verification
- Conditional Access troubleshooting
- Endpoint security verification

The project should now prioritize **depth and realistic scenarios over adding many more isolated configuration tasks**.

---

## Recommended Next Phase

If the environment is still available, prioritize only high-value gaps:

1. **Microsoft Purview / Compliance** — if the current subscription exposes the required capabilities.
2. **Windows Autopilot** — to extend the Intune device lifecycle.
3. **Integrated Microsoft 365 administration scenario** — onboarding, access, endpoint, security, verification, and offboarding.

PowerShell automation should be treated as a separate infrastructure skill when a suitable environment is available.

---

# Repository Structure

```text
microsoft-365-enterprise-lab/
│
├── README.md
│
├── Architecture/
│   ├── README.md
│   └── m365-enterprise-topology.svg
│
└── Documentation/
    ├── 01-tenant-organization-setup.md
    ├── 02-entra-id-users-groups.md
    ├── 03-entra-id-administration-security.md
    ├── 04-exchange-online-mailboxes.md
    ├── 05-exchange-mail-flow-troubleshooting.md
    ├── 06-microsoft-teams.md
    ├── 07-sharepoint-online.md
    ├── 08-onedrive.md
    ├── 09-intune-device-enrollment.md
    ├── 10-intune-configuration-compliance.md
    ├── 11-intune-application-endpoint-management.md
    ├── 12-conditional-access.md
    └── 13-microsoft-defender.md
```

---

## Status

**13 practical Microsoft 365 administration tasks completed.**

The repository is intended to show **hands-on administration + verification + troubleshooting**, not course completion.

**Primary career relevance:** IT Infrastructure / Microsoft 365 / Endpoint Administration / Junior Systems Administration
