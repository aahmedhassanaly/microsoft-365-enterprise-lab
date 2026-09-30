# Task 10 — Intune Configuration & Compliance

## Objective

In this task, I configured Microsoft Intune to apply Windows security settings and verify that the device follows the required security rules.

The main goal was to understand the difference between:

- Configuration Profile — applies and enforces settings.
- Compliance Policy — checks whether the device meets security requirements.

Environment:

- Microsoft Intune
- Windows 10/11
- Device: `DESKTOP-2J1L8D5`
- Model: Dell Precision 5520
- Ownership: Personal
- Primary User: Ahmed Hassan
- Management: Intune

---

## 1. Create Configuration Profile

Navigate to:

Intune Admin Center → Devices → Manage devices → Configuration → Create

Select:

- Platform: Windows 10 and later
- Profile type: Settings catalog

Profile:

- Name: `Kozika-Windows-Security`
- Description: `Basic security configuration for Kozika Windows devices`

### Firewall Configuration

In Settings Catalog, search for `Firewall`.

The following settings were enabled:

- Enable Domain Network Firewall = True
- Enable Private Network Firewall = True
- Enable Public Network Firewall = True

Default actions:

- Inbound = Block
- Outbound = Allow

Other advanced firewall settings were left unchanged.
<img width="1898" height="842" alt="image" src="https://github.com/user-attachments/assets/4b299f32-93b5-4f24-b5fa-d7a4c867d3ab" />

---

## 2. Assign the Configuration Profile

The profile was assigned to the required device scope.

After assignment, the device checked in with Intune.

Navigate to:

Kozika-Windows-Security → Monitor → Device and user check-in status

Result:

- User: `ahmed.hassan@kozika.online`
- Status: Succeeded

This confirmed that the configuration profile was successfully applied.
<img width="1918" height="873" alt="image" src="https://github.com/user-attachments/assets/1bd62d55-2cff-45a9-a98e-2e84fd9ece42" />

---

## 3. Verify Firewall Enforcement

The Windows Firewall was already enabled on the device.

To verify that Intune was actually enforcing the configuration, the firewall was manually turned off.

After Intune applied the configuration again, the firewall returned to the required enabled state.

This provided a practical test that the Configuration Profile was not only created but was also being applied to the managed device.
<img width="1376" height="986" alt="image" src="https://github.com/user-attachments/assets/5807f498-1fe0-4355-b102-3553fc6882ae" />

---

## 4. Create Compliance Policy

Navigate to:

Intune Admin Center → Devices → Compliance policies → Policies → Create

Select:

- Platform: Windows 10 and later
- Profile type: Windows 10/11 compliance policy

Policy:

- Name: `Kozika-Windows-Compliance`
- Description: `Basic compliance requirements for Kozika Windows devices`

---

## 5. Configure Compliance Requirements

The following requirements were configured as **Required**:

### System Security

- Firewall = Required
- Antivirus = Required
- Antispyware = Required
- Microsoft Defender Antimalware = Required
- Microsoft Defender Antimalware security intelligence up-to-date = Required
- Real-time protection = Required

Other settings such as:

- BitLocker
- Secure Boot
- TPM
- Password requirements
- Code Integrity
- Device Properties
- Defender for Endpoint risk

were left as Not configured for this lab.

This kept the policy focused on the required Windows security controls.
<img width="1919" height="892" alt="image" src="https://github.com/user-attachments/assets/e7b96db9-e5ed-41a6-9766-f06fe891a30b" />

---

## 6. Configure Noncompliance Action

The policy was configured to:

- Mark device noncompliant
- Immediately

No additional notification template was configured.

---

## 7. Assign Compliance Policy

The compliance policy was assigned to:

- All Devices

No exclusions were configured.

The device was then synchronized with Intune to request the latest policy.

---

## 8. Monitor Compliance

Navigate to:

Kozika-Windows-Compliance → Monitor → Per setting status

The initial evaluation showed some Defender-related compliance problems.

The device reported that Microsoft Defender security intelligence was out of date.

Windows Security was checked on the device and confirmed that the protection definitions were outdated.

### Troubleshooting Process

Problem:

Defender security intelligence was not compliant.

Evidence:

Windows Security showed that protection definitions were out of date.

Fix:

Updated Microsoft Defender security intelligence from Windows Security.

Verification:

After Intune evaluated the device again, all required settings became compliant.

Final result:

- Microsoft Defender Antimalware security intelligence = Compliant
- Real-time protection = Compliant
- Microsoft Defender Antimalware = Compliant
- Antivirus = Compliant
- Antispyware = Compliant
- Firewall = Compliant

---

<img width="1916" height="888" alt="image" src="https://github.com/user-attachments/assets/23c5df21-f0ed-4d87-b823-b04bc5259dac" />

## 9. Configuration vs Compliance

The main concept learned in this task:

### Configuration Profile

Configuration Profile means:

> "Do this."

It applies settings to the device.

Example:

`Enable Windows Firewall`

### Compliance Policy

Compliance Policy means:

> "Are you doing it?"

It checks the device and reports whether the required settings are satisfied.

Example:

`Firewall must be enabled`

A simple way to remember:

**Configuration = Apply**

**Compliance = Check**

Later, Conditional Access can use the compliance result to control access to company resources.

---

## 10. Troubleshooting Method

The troubleshooting process used in this task was:

**Problem → Evidence → Hypothesis → Test → Fix → Verify**

Example:

Problem:
Defender was reported as not compliant.

Evidence:
Windows Security showed outdated protection definitions.

Hypothesis:
The Defender security intelligence requirement was failing because the definitions were outdated.

Test:
Check Windows Security and update Defender definitions.

Fix:
Update the security intelligence.

Verify:
Wait for Intune to evaluate the device again.

Result:
All compliance checks became Compliant.

---

## 11. Final Verification

Final device state:

- Device enrolled in Intune
- Configuration Profile applied successfully
- Windows Firewall enabled
- Compliance Policy assigned
- Defender protection active
- Security intelligence up to date
- All compliance requirements = Compliant

The configuration profile and compliance policy were both successfully tested on the managed Windows device.

---

## Skills Practiced

- Creating Intune Configuration Profiles
- Using Settings Catalog
- Configuring Windows Firewall
- Assigning Intune policies
- Monitoring policy status
- Creating Compliance Policies
- Configuring Defender compliance requirements
- Understanding All Devices assignment
- Reading per-setting compliance results
- Troubleshooting Intune compliance
- Understanding Configuration vs Compliance
- Verifying policy enforcement on a real managed device

---

## Task Result

**Task 10 — Intune Configuration & Compliance: COMPLETED**

The lab successfully demonstrated how Intune can configure Windows security settings, evaluate device compliance, report problems, and reapply required configuration.
