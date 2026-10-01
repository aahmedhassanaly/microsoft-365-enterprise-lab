# Task 11 — Intune Application & Endpoint Management

## Objective

The objective of this task was to learn how to deploy, monitor, detect, and uninstall applications using Microsoft Intune.

The lab focused on a real Endpoint Management workflow:

Create → Assign → Install → Detect → Monitor → Uninstall → Verify

---

## Environment

- Microsoft Intune
- Windows 10/11 device
- Device: `DESKTOP-2J1L8D5`
- User: `ahmed.hassan@kozika.online`
- Microsoft Intune Management Extension (IME)
- Win32 application: 7-Zip
- Microsoft Store application: NanaZip

---





## Win32 Application Deployment

The main Endpoint Management exercise used 7-Zip as a Win32 application.

### Application Information

- Name: `7-Zip`
- Publisher: `Igor Pavlov`
- Package: `7z2603-x64.intunewin`
- Install behavior: System
- Minimum OS: Windows 10 20H2
- Architecture: x86, x64

### Install Command

    7z2603-x64.exe /S

### Uninstall Command

    "%ProgramFiles%\7-Zip\Uninstall.exe" /S

---

## 3. Win32 Package Creation

The Microsoft Win32 Content Prep Tool was used to convert the 7-Zip installer into an Intune package.

The generated package was:

    7z2603-x64.intunewin

This package was uploaded to Intune when creating the Win32 application.

---

## 4. Detection Rule

A file-based detection rule was configured.

### Detection

- Path:

    C:\Program Files\7-Zip

- File:

    7zFM.exe

The detection rule allows Intune to determine whether the application is installed on the device.

This is important because Intune needs a reliable detection method to decide whether the required application is already installed.

---

## 5. Requirements

The following requirements were configured:

- Operating system architecture: x86, x64
- Minimum Windows version: Windows 10 20H2
- Additional disk, memory, and CPU requirements: Not configured

---

## 6. Assignment

The 7-Zip application was assigned as:

- Assignment type: Required
- Group: All devices
- Filter: None
- Installation: As soon as possible
- User notifications: Show all toast notifications
- Restart grace period: Disabled
- Content download: In background

The application was successfully deployed to the device.

---

## 7. Verify Installation on the Device

The installation was verified directly on Windows.

PowerShell command:

    Get-Item "C:\Program Files\7-Zip\7zFM.exe" -ErrorAction SilentlyContinue

The file was found, confirming that 7-Zip was installed.

This was used as direct device evidence instead of relying only on the Intune portal.

---
<img width="1919" height="815" alt="image" src="https://github.com/user-attachments/assets/b1e95505-475c-4605-a9af-3bf8ba7c4887" />


## 8. Intune Management Extension

The Microsoft Intune Management Extension was verified on the Windows device.

PowerShell command:

    Get-Service IntuneManagementExtension

The service was found running.

The IME is important for Win32 application deployment and processing application policies on Windows devices.

---

## 9. Troubleshooting Using IME Logs

The following log was used:

    C:\ProgramData\Microsoft\IntuneManagementExtension\Logs\AppWorkload.log

The log showed the application policies received by the device.

For 7-Zip, the log contained:

- Application ID
- Detection rule
- Install command
- Uninstall command
- Requirements
- Package information

For NanaZip, the log showed:

- Detection as `NotDetected`
- Applicability as `Applicable`
- Installation started
- Download in progress
- Enforcement state `InProgress`

This demonstrated how the IME log can be used to determine what Intune is actually doing on the device.

---

## 10. Uninstall Test

After confirming that 7-Zip was installed, an uninstall test was performed.

The Required assignment was removed first to avoid assigning conflicting intents to the same device.

The application was then assigned with:

- Assignment type: Uninstall
- Group: All devices
- Filter: None

7-Zip was removed from the Windows device.

The following PowerShell command was used to verify the result:

    Get-Item "C:\Program Files\7-Zip\7zFM.exe" -ErrorAction SilentlyContinue

No output was returned.

This confirmed that the 7-Zip executable was no longer present on the device.
<img width="1909" height="869" alt="image" src="https://github.com/user-attachments/assets/b6fb957e-8947-4bb1-b31f-6d734fded0ca" />
<img width="1907" height="879" alt="image" src="https://github.com/user-attachments/assets/3159768f-fcf1-4def-91e3-7905ecba7716" />

---

## 11. Monitoring

The Intune application monitoring page showed:

- Device status: 1
- Installed: 1
- Not Installed: 0
- Failed: 0
- Install Pending: 0
- Not Applicable: 0

The device itself was also checked directly.

This demonstrated an important Endpoint Management concept:

Intune reporting should be compared with actual device evidence when troubleshooting.

Portal status alone should not always be treated as proof that the application is physically present on the device.

---<img width="1919" height="877" alt="image" src="https://github.com/user-attachments/assets/4cd90bf1-41fb-4b2a-9b25-bdcac993eb8a" />


## 12. Troubleshooting Method

The following troubleshooting process was used:

### Problem

The application was not visible on the Windows device.

### Evidence

- Intune assignment status
- Windows installed applications
- PowerShell detection
- IME service
- `AppWorkload.log`

### Hypothesis

The application deployment process had not completed successfully or was still being processed.

### Test

The IME log was checked to determine the actual application state and installation activity.

### Fix

The application assignment and deployment state were corrected and the device was allowed to process the policy.

### Verify

The application was checked directly on Windows using the detection file.

---

## Skills Practiced

- Microsoft Intune application management
- Microsoft Store application deployment
- Win32 application deployment
- Win32 Content Prep Tool
- Application assignments
- Required deployment
- Uninstall assignment
- Detection rules
- Microsoft Intune Management Extension
- Application monitoring
- IME log analysis
- PowerShell verification
- Application troubleshooting

---

## Task Result

**COMPLETED**

The lab demonstrated a complete Win32 application lifecycle:

**Package → Deploy → Install → Detect → Monitor → Uninstall → Verify**

The next part of Endpoint Management should focus on deeper application troubleshooting and deployment behavior rather than creating many additional test applications.
