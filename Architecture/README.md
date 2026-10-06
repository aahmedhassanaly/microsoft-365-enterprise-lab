# Architecture

This directory contains the architecture documentation and topology diagram for the Microsoft 365 Enterprise Lab.

## Topology Image

Reserved path for the final topology image:

`m365-enterprise-topology.png`

The image should show:

1. **On-premises**
   - Windows Server / Active Directory
   - Domain: `kozika.local`
   - Users and security groups
   - Microsoft 365 OU

2. **Identity synchronization**
   - Microsoft Entra Cloud Sync
   - Password Hash Synchronization

3. **Microsoft cloud**
   - Microsoft Entra ID
   - Exchange Online
   - Microsoft Teams
   - SharePoint Online
   - OneDrive for Business
   - Microsoft Intune
   - Conditional Access
   - Microsoft Defender

4. **Managed endpoint**
   - Windows 11
   - Microsoft Entra Registered
   - Intune Managed
   - Compliance
   - Defender protection

## Logical Flow

```text
┌──────────────────────────────┐
│ On-Premises Windows Server   │
│ Active Directory             │
│ kozika.local                │
└──────────────┬───────────────┘
               │
               │ Cloud Sync
               │ + PHS
               ▼
┌──────────────────────────────┐
│ Microsoft Entra ID           │
│ Identity + RBAC + MFA        │
└───────┬───────────┬──────────┘
        │           │
        │           └─────────────────────┐
        ▼                                 ▼
┌──────────────────────┐       ┌──────────────────────┐
│ Microsoft 365        │       │ Microsoft Intune     │
│ Workloads            │       │ Endpoint Management  │
│                      │       └──────────┬───────────┘
│ Exchange Online      │                  │
│ Teams                │                  ▼
│ SharePoint Online    │       ┌──────────────────────┐
│ OneDrive             │       │ Windows 11 Endpoint  │
└──────────┬───────────┘       │ Entra Registered     │
           │                   │ Intune Managed       │
           │                   │ Compliant            │
           ▼                   └──────────┬───────────┘
┌──────────────────────┐                  │
│ Conditional Access   │◄─────────────────┘
│ MFA + Device State   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ Microsoft Defender   │
│ Endpoint + Antivirus │
└──────────────────────┘
```

The PNG topology is intentionally kept separate from the task documentation so the architecture can be updated without changing the individual task write-ups.
