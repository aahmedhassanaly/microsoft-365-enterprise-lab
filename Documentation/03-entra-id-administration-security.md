# 03 - Entra ID Administration & Security

## Objective

The goal of this task was to practice Microsoft Entra ID administration and security using the existing Kozika environment.

The main objectives were:

- Understand Entra ID administrative roles
- Apply Least Privilege
- Configure Microsoft Authenticator
- Test MFA
- Create an Administrative Unit
- Assign an administrative role with a limited scope
- Verify permissions and troubleshoot an administration issue

---

## Environment

- Microsoft Entra ID
- Microsoft 365 Tenant: `kozika12.onmicrosoft.com`
- Custom Domain: `kozika.online`
- On-Premises AD Domain: `kozika.local`
- Microsoft Entra Cloud Sync
- Password Hash Synchronization enabled
- Users synchronized from Windows Server AD

Main administrative accounts:

- Ahmed Hassan — Global Administrator
- Omar Khaled — User Administrator

---

## 1. Entra ID Roles

The first step was to review Entra ID directory roles.

The lab started with Ahmed Hassan using the Global Administrator role.

Global Administrator was used for tenant-level configuration because this lab account is responsible for the complete Microsoft 365 environment.

A second administrator was created using the existing user:

`omar.khaled@kozika.online`

Omar was assigned:

`User Administrator`

This was used to practice the Least Privilege principle instead of using Global Administrator for normal user administration.

---

## 2. Least Privilege

The lab used two different administrative levels:

Ahmed:

`Global Administrator`

Omar:

`User Administrator`

The purpose was to avoid giving every administrator full tenant-level permissions.

Omar was successfully able to access Entra ID and manage users.

For example, Omar could open user profiles and access administrative actions such as password reset.

---

## 3. Microsoft Authenticator

Microsoft Authenticator was configured through:

Entra ID → Authentication methods → Policies → Microsoft Authenticator

The policy was scoped to:

`GG-Sales`

Omar is a member of `GG-Sales`.

The following settings were used:

- Enable: Yes
- Target: Selected group
- Group: `GG-Sales`
- Registration: Optional
- Authentication mode: Any

This configuration made Microsoft Authenticator available for the targeted users.

---

## 4. Microsoft Authenticator Registration

Omar registered Microsoft Authenticator using:

`https://mysignins.microsoft.com/security-info`

The registration was completed successfully.

The authentication methods for Omar were then checked in:

Entra ID → Users → Omar Khaled → Authentication methods

Microsoft Authenticator appeared as a registered authentication method.

---

## 5. MFA Verification

A real sign-in test was performed using Omar's account.

During Microsoft 365 sign-in, Entra ID requested an additional verification step.

The sign-in displayed a number matching request.

Omar approved the request using Microsoft Authenticator.

This verified that the configured authentication flow successfully requested an additional authentication factor during the test sign-in.

Important distinction:

Registering an authentication method and enforcing MFA are different concepts. The lab verified the actual MFA challenge during this sign-in test.

---<img width="1919" height="871" alt="image" src="https://github.com/user-attachments/assets/f248e8bf-cdcf-474e-8cc2-f3630597680a" />


## 6. Administrative Unit

An Administrative Unit was created:

`AU-Sales`

The purpose was to create a limited administrative scope.

The Administrative Unit was then configured with users for testing.

Omar was added to `AU-Sales`.

Nada Mohamed was also added temporarily for permission testing.

---<img width="1919" height="855" alt="image" src="https://github.com/user-attachments/assets/d5451642-5bdb-40db-8b0a-9f1b9eac1a6c" />


## 7. Scoped User Administrator

Omar initially had:

`User Administrator → Directory`

This gave him a directory-wide User Administrator assignment.

To practice Least Privilege, a second assignment was created:

`User Administrator → AU-Sales`

After the AU-scoped assignment was created, the original directory-wide assignment was removed.

Final configuration:

Ahmed:

`Global Administrator → Directory`

Omar:

`User Administrator → AU-Sales`

This created a more restricted administrative model.
<img width="1914" height="884" alt="image" src="https://github.com/user-attachments/assets/24b92e66-1203-4cde-ab9b-5656f77beea8" />

---

## 8. Permission Testing

A permission test was performed using Omar's account.

### Test 1 - User Outside the AU

Omar attempted to reset the password of Sara Ali.

Sara was not a member of `AU-Sales`.

The operation failed with:

`The password can not be reset. This may be due to an incorrect level of administrative privilege or if trying to reset your own password.`

This confirmed that Omar could not perform the tested administrative action outside his assigned Administrative Unit.
<img width="1910" height="916" alt="image" src="https://github.com/user-attachments/assets/c96061eb-bc27-4b7c-9ac0-1a82d938aed8" />

---

### Test 2 - User Inside the AU

Nada Mohamed was added to:

`AU-Sales`

Omar then attempted to reset Nada's password.

The operation reached the password reset stage but returned:

`Unfortunately, you cannot reset this user's password because password writeback is not enabled in your tenant.`

Nada is a synchronized on-premises user.

The error indicates that the password reset requires Password Writeback to send the new password from Microsoft Entra ID back to the on-premises Active Directory.

Password Writeback was not enabled as part of this task.

We did not enable it because Password Writeback is outside the main objective of this Entra administration and security task.

The result still provided useful evidence that Omar's scoped administration reached the user inside the Administrative Unit.
<img width="1919" height="1007" alt="image" src="https://github.com/user-attachments/assets/796e9e0d-89d5-4831-9230-4650cbeb3773" />

---

## 9. Troubleshooting

### Problem

Omar could not reset a synchronized user's password.

### Evidence

Entra ID displayed:

`password writeback is not enabled in your tenant`

### Analysis

The user is synchronized from:

`kozika.local`

The password reset therefore requires a supported password writeback configuration if the password must be written back to the on-premises Active Directory.

### Decision

Password Writeback was not enabled during this task.

It will be treated as a separate hybrid identity configuration topic.

---

## 10. Final Configuration

### Administrator

Ahmed Hassan

`Global Administrator`

Scope:

`Directory`

### Scoped Administrator

Omar Khaled

`User Administrator`

Scope:

`AU-Sales`

### Authentication

Microsoft Authenticator:

`Registered for Omar`

MFA test:

`Number matching successfully completed`

### Administrative Unit

`AU-Sales`

---

## Key Skills Practiced

- Entra ID directory roles
- Global Administrator
- User Administrator
- Least Privilege
- Microsoft Authenticator
- MFA verification
- Authentication methods
- Administrative Units
- Scoped administration
- Permission testing
- Password Writeback troubleshooting
- Hybrid identity administration

---

## Important Lessons

1. Do not use Global Administrator for every administrative task.
2. Administrative Units can be used to create a limited administrative scope.
3. Authentication method registration is different from MFA enforcement.
4. Permission testing is required after changing administrative roles.
5. Synchronized users have different password-reset requirements from cloud-only users.
6. Password Writeback is required when a cloud password reset must be written back to on-premises Active Directory.

---

## Final Result

Task 03 was completed successfully.

The Kozika Microsoft 365 environment now has:

- A Global Administrator for tenant-level administration
- A scoped User Administrator for `AU-Sales`
- Microsoft Authenticator configured for the Sales group
- Successful MFA verification for Omar
- An Administrative Unit for Sales administration
- Practical permission testing
- Troubleshooting experience with Password Writeback

**Task Status: COMPLETED**
