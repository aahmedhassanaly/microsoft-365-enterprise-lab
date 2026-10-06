# Architecture

This directory contains the architecture documentation and topology diagram for the Microsoft 365 Enterprise Lab.

## Topology

![Microsoft 365 Enterprise Lab Topology](m365-enterprise-topology.svg)


## What the diagram represents

1. **On-premises**
   - Windows Server / Active Directory
   - Domain: `kozika.local`
   - Users and security groups
   - Microsoft 365 synchronization OU

2. **Identity synchronization**
   - Microsoft Entra Provisioning Agent
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

## Logical flow

```text
Active Directory (kozika.local)
        │
        │ Cloud Sync + PHS
        ▼
Microsoft Entra ID
        │
        ├── Exchange Online
        ├── Teams / SharePoint / OneDrive
        ├── Intune
        └── Conditional Access / Defender
                    │
                    ▼
              Windows 11
        Entra Registered / Intune Managed
                    │
                    ▼
            Endpoint Security
```
