# Task 04 — Exchange Online & Mailboxes

## Objective

Configure and manage Exchange Online mailboxes in Microsoft 365.

The goal of this task is to understand mailbox configuration, email addresses, mailbox storage, mail flow settings, and basic email connectivity.

---

## Environment

- Microsoft 365 Tenant: `kozika12.onmicrosoft.com`
- Custom Domain: `kozika.online`
- Exchange Online
- Primary Test User: Ahmed Hassan
- Primary Email: `ahmedhassan@kozika.online`

---

## 1. Exchange Online License

The Microsoft 365 tenant had one active Microsoft 365 Business Premium with Copilot license.

The license was already assigned to the primary tenant administrator account, so no additional license was purchased.

The licensed account was used to test Exchange Online functionality.

---

## 2. Exchange Online Mailbox

The mailbox was checked from:

Exchange Admin Center → Recipients → Mailboxes

Ahmed Hassan appeared as a User Mailbox.

Mailbox details:

- Display Name: `ahmed hassan`
- Alias: `ahmedhassan`
- Primary Email: `ahmedhassan@kozika.online`
- User ID: `ahmedhassan@kozika12.onmicrosoft.com`

The mailbox was active and accessible through Outlook on the web.
<img width="1854" height="887" alt="image" src="https://github.com/user-attachments/assets/71134605-27d3-42bb-aab1-fccacc4df5b9" />

---

## 3. MX Record Configuration

Initially, the domain used Cloudflare Email Routing.

The MX records pointed to:

- `route1.mx.cloudflare.net`
- `route2.mx.cloudflare.net`
- `route3.mx.cloudflare.net`

Because of this, external incoming email was not reaching Exchange Online.

Cloudflare Email Routing was disabled.

The Microsoft 365 MX record was then configured:

- Type: `MX`
- Name: `@`
- Mail Server: `kozika-online.mail.protection.outlook.com`
- Priority: `1`

After the change, external email was successfully delivered to the Microsoft 365 mailbox.
<img width="1911" height="1025" alt="image" src="https://github.com/user-attachments/assets/c0398b4d-f61c-4f2d-807f-0423910d5384" />

---

## 4. Mailbox Contact Information

The mailbox contact information was reviewed.

- First Name: `ahmed`
- Last Name: `hassan`
- Display Name: `ahmed hassan`
- Alias: `ahmedhassan`
- Hide from GAL: No

The mailbox is visible in the Global Address List.

---

## 5. Email Addresses

The mailbox contains different address types.

### Primary SMTP

`ahmedhassan@kozika.online`

The uppercase `SMTP` identifies the primary SMTP address.

This is the main email address used by the mailbox.

### Secondary SMTP Alias

`ahmedhassan@kozika12.onmicrosoft.com`

The lowercase `smtp` identifies a secondary proxy address.

Mail sent to this address is delivered to the same mailbox.

### SIP

`ahmedhassan@kozika12.onmicrosoft.com`

The SIP address is used for communication services and is not a normal email address.

### SPO

The mailbox also contains an internal SharePoint-related SPO address.

This address is used by Microsoft 365 services and is not used as a normal email address.

---<img width="1907" height="852" alt="image" src="https://github.com/user-attachments/assets/d8053b42-bc6b-4947-bdbd-1f7413839cba" />


## 6. Mailbox Usage

Mailbox usage was checked.

Current usage:

- Used: `1.73 MB`
- Mailbox capacity shown: `99 GB`
- Usage: `0.00%`

Mailbox storage is different from message size.

### Mailbox Storage

Controls the total amount of data stored inside the mailbox.

### Message Size Restriction

Controls the size of an individual email message, including its content and attachments.

The message size restriction was shown as Unlimited and was not changed.

---

## 7. Email Forwarding

Email forwarding was checked.

Current setting:

- Forwarding: Disabled

This means incoming messages are not automatically forwarded to another email address.

When forwarding is configured, a message can be delivered to the mailbox and also forwarded to another address, depending on the forwarding configuration.

No forwarding was configured for this lab mailbox.

---

## 8. Message Delivery Restrictions

The mailbox delivery restrictions were reviewed.

Current configuration:

- Accept messages from: All senders
- Reject messages from: None

This means the mailbox is not configured with a custom sender restriction.

No changes were required.

---

## 9. Email Applications

The mailbox email application settings were reviewed.

Available services included:

- Outlook desktop (MAPI)
- Exchange Web Services (EWS)
- Mobile (Exchange ActiveSync)
- IMAP
- POP3
- Outlook on the web (OWA)
- Outlook Web App mailbox policy

These settings control how applications and devices can connect to the mailbox.

No unnecessary changes were made during this task.

---

## 10. Mailbox Testing

The mailbox was tested using external email.

Test flow:

External Email
→ `ahmedhassan@kozika.online`
→ Exchange Online
→ Ahmed Mailbox
→ Reply
→ External Sender

The test was successful.

### Result

- External → Microsoft 365: Successful
- Microsoft 365 → External: Successful
- Reply from Microsoft 365 → External: Successful

This confirmed that the basic inbound and outbound mail flow was working after the MX record change.
<img width="1906" height="870" alt="image" src="https://github.com/user-attachments/assets/39df7c08-97d1-46e3-a68f-e769b3fba15e" />

---

## 11. Troubleshooting Finding

The main issue found during this task was the MX configuration.

### Problem

External emails were not reaching Exchange Online.

### Evidence

The domain MX records pointed to Cloudflare Email Routing.

### Root Cause

Cloudflare Email Routing was active and handling the domain MX records.

### Fix

1. Disabled Cloudflare Email Routing.
2. Removed the Cloudflare Email Routing MX records.
3. Added the Microsoft 365 MX record.
4. Tested external email delivery.

### Verification

External email successfully reached the Exchange Online mailbox.

---

## Final Configuration

The final mailbox configuration was:

- Exchange Online mailbox: Active
- Primary SMTP: `ahmedhassan@kozika.online`
- Secondary SMTP: `ahmedhassan@kozika12.onmicrosoft.com`
- Mailbox usage: `1.73 MB / 99 GB`
- Email forwarding: Disabled
- Delivery restrictions: None
- External inbound mail: Working
- External outbound mail: Working
- MX: Microsoft 365

---

## Key Skills Practiced

- Exchange Online mailbox administration
- Primary and secondary SMTP addresses
- Mailbox storage
- Message size restrictions
- Email forwarding
- Message delivery restrictions
- MAPI, EWS, ActiveSync, IMAP, POP3 and OWA
- MX record troubleshooting
- Basic inbound and outbound mail flow testing
- Exchange Online troubleshooting

---

## Task Status

**COMPLETED**

Next task:

**Task 05 — Exchange Mail Flow & Troubleshooting**
