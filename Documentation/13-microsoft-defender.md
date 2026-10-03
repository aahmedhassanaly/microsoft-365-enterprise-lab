# Task 13 — Microsoft Defender

## Objective

Configure and verify Microsoft Defender for Endpoint and Microsoft Defender Antivirus using Microsoft Intune.

The goal was to manage endpoint security centrally and verify that the security policy was actually applied to the Windows device.

---

## Environment

- Microsoft Intune
- Microsoft Defender for Endpoint
- Microsoft Defender Antivirus
- Windows 11 endpoint
- Device: `DESKTOP-2J1L8D5`
- User: `ahmed.hassan@kozika.online`
- Management: Microsoft Intune
- Device onboarding group: `MDB Windows device onboarding group`

---

## 1. Defender for Endpoint Onboarding

The Windows device was onboarded to Microsoft Defender for Business through the Microsoft Defender portal.

The Defender setup connected Microsoft Defender for Endpoint with Microsoft Intune.

The device was added to the onboarding process through:

    Microsoft Defender Portal
    → Add Windows devices
    → Select the Intune-managed device

The onboarding group used by Intune was:

    MDB Windows device onboarding group

The group contained:

    1 device
    0 users

---

## 2. Verify Defender Device Inventory

After synchronization, the device appeared in Microsoft Defender Device Inventory.

Device information:

- Device: `desktop-2j1l8d5`
- Operating System: Windows 11 25H2
- Device Type: Workstation
- Product: Defender for Endpoint
- Security Management: Intune
- Status: Active
- Onboarding Status: Onboarded
- Known Risk: None

This confirmed that the endpoint was successfully onboarded to Defender for Endpoint.

---<img width="1911" height="844" alt="image" src="https://github.com/user-attachments/assets/f35137c4-c2a3-4e25-8c95-7948fb4339d3" />


## 3. Create Microsoft Defender Antivirus Policy

Created an Intune Antivirus policy:

    Name:
    Kozika-Defender-Antivirus

    Description:
    Microsoft Defender Antivirus security policy for Kozika Windows devices

    Platform:
    Windows

    Profile:
    Microsoft Defender Antivirus

The policy was assigned to:

    MDB Windows device onboarding group

Assignment:

- Included: Yes
- Exclusions: None
- Filter: None
- Scope Tag: Default

---

## 4. Defender Antivirus Configuration

The policy included practical Microsoft Defender Antivirus settings.

Configured settings included:

- Allow Behavior Monitoring
- Allow Cloud Protection
- Allow Email Scanning
- Allow Full Scan On Mapped Network Drives
- Allow Full Scan Removable Drive Scanning
- Allow scanning of all downloaded files and attachments
- Allow Realtime Monitoring
- Allow Scanning Network Files
- Allow Script Scanning
- Allow On Access Protection

Additional Defender settings were reviewed but were not changed unless required for the lab.

Security exclusions such as:

- Excluded Extensions
- Excluded Paths
- Excluded Processes

were left unconfigured.

Advanced update and scheduling settings were also not changed.

---
<img width="1917" height="848" alt="image" src="https://github.com/user-attachments/assets/e3ce4e3f-01f5-4aa8-89ed-77184a2747bb" />

## 5. Monitor Policy Deployment

The policy was deployed through Microsoft Intune.

The device check-in status showed:

    Device:
    DESKTOP-2J1L8D5

    Logged-in user:
    ahmed.hassan@kozika.online

    Check-in status:
    Success

The Per Setting Status showed:

    Succeeded: 1
    Error: 0
    Conflict: 0
    Not applicable: 0
    In Progress: 0

This confirmed that the Antivirus policy was successfully delivered to the endpoint.

---

## 6. Endpoint Verification with PowerShell

The actual Defender status was verified locally on the Windows endpoint.

Command:

    Get-MpComputerStatus | Select-Object RealTimeProtectionEnabled,BehaviorMonitorEnabled,AntivirusEnabled,AntispywareEnabled

Result:

    RealTimeProtectionEnabled    True
    BehaviorMonitorEnabled       True
    AntivirusEnabled             True
    AntispywareEnabled           True

This confirmed that the Defender Antivirus configuration was active on the endpoint.

<img width="1458" height="715" alt="image" src="https://github.com/user-attachments/assets/44d628c3-725d-4d0d-b139-6309a0e7b319" />
---

## 7. Windows Security Verification

Windows Security was also checked from the endpoint.

Virus & threat protection showed:

- No current threats
- No action needed
- Security intelligence is up to date
- Quick Scan completed successfully
- 0 threats detected

The Virus & threat protection settings showed:

- Real-time protection: On
- Cloud-delivered protection: On
- Automatic sample submission: On

The Windows Security interface also showed:

    This setting is managed by your administrator.

This confirmed that the security configuration was being managed centrally.
<img width="1210" height="953" alt="image" src="https://github.com/user-attachments/assets/25b29eeb-4821-4c6d-997a-55331545ce41" />

---



## . Troubleshooting Method

The task followed a practical troubleshooting flow:

    Problem
    ↓
    Check Intune policy
    ↓
    Check device assignment
    ↓
    Check policy check-in
    ↓
    Verify Defender status on endpoint
    ↓
    Verify Windows Security
    ↓
    Confirm final state

Important evidence used during verification:

- Defender Device Inventory showed the device as Onboarded.
- Intune showed successful policy deployment.
- PowerShell showed Defender protection enabled.
- Windows Security showed no active threats.
- Security intelligence was up to date.

---

## 10. What I Learned

### Microsoft Defender for Endpoint

Provides endpoint security monitoring and protection.

### Microsoft Defender Antivirus

Provides malware and threat protection on Windows devices.

### Microsoft Intune

Allows administrators to centrally configure and manage Defender settings on managed endpoints.

### Defender Onboarding

Connects the Windows endpoint to Microsoft Defender for Endpoint.

### Antivirus Policy

Defines the Defender Antivirus configuration that should be applied to managed devices.

### Policy Deployment

Intune sends the configuration to the assigned device.

### Endpoint Verification

The administrator should not depend only on the Intune policy status.

The actual endpoint should also be checked.

---

## 11. Final Verification

The following requirements were completed:

- Microsoft Defender for Endpoint onboarding: Completed
- Device visible in Defender Device Inventory: Completed
- Defender Antivirus policy created: Completed
- Policy assigned to device: Completed
- Intune policy deployment: Successful
- Defender Antivirus enabled: Verified
- Real-time protection enabled: Verified
- Behavior monitoring enabled: Verified
- Antispyware enabled: Verified
- Cloud protection enabled: Verified
- Windows Security verification: Completed
- Threat status: No active threats
- Security intelligence: Up to date

---

## Task Result

**COMPLETED**

The endpoint is onboarded to Microsoft Defender for Endpoint and Microsoft Defender Antivirus is centrally managed through Microsoft Intune.
