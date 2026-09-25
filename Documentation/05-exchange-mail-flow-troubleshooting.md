# Task 05 - Exchange Mail Flow & Troubleshooting

## Objective

The goal of this task is to configure and troubleshoot Exchange Online mail flow.

In this lab, we worked with:

- SPF
- DKIM
- DMARC
- Message Trace
- Mail Flow Rules
- External email warning
- Mail delivery troubleshooting

The main goal was to understand how an Exchange Administrator can investigate email delivery problems using real evidence.

---

## Environment

- Microsoft 365 Tenant: `kozika12.onmicrosoft.com`
- Custom Domain: `kozika.online`
- Exchange Online
- DNS Provider: Cloudflare
- Primary Test Mailbox: `ahmedhassan@kozika.online`
- External Test Mailbox: Gmail

---

# 1. SPF Configuration

An SPF record defines which mail systems are allowed to send email for a domain.

The following SPF record was configured in Cloudflare:

    v=spf1 include:spf.protection.outlook.com -all

### Important Parts

- `v=spf1` - Defines the SPF record.
- `include:spf.protection.outlook.com` - Allows Microsoft 365 mail servers to send email.
- `-all` - Other senders should fail SPF validation.

Only one SPF record should exist for the domain.

### Result

SPF was successfully configured for:

    kozika.online

---
<img width="1475" height="402" alt="image" src="https://github.com/user-attachments/assets/fa95b359-f415-4cb0-ba44-59d39a97c221" />

# 2. DKIM Configuration

DKIM adds a digital signature to outgoing email.

The purpose of DKIM is to help receiving mail systems verify that the message was sent by an authorized system and that important parts of the message were not changed.

Microsoft 365 provided two CNAME records for the custom domain.

### Selector 1

    selector1._domainkey.kozika.online

Target:

    selector1-kozika-online._domainkey.kozika12.p-v1.dkim.mail.microsoft

### Selector 2

    selector2._domainkey.kozika.online

Target:

    selector2-kozika-online._domainkey.kozika12.p-v1.dkim.mail.microsoft

Both records were configured in Cloudflare as:

    DNS Only

### DNS Verification

The records were verified using `nslookup`.

    nslookup -type=CNAME selector1._domainkey.kozika.online

The result returned the expected Microsoft target.

The second selector was also verified:

    nslookup -type=CNAME selector2._domainkey.kozika.online

Both CNAME records resolved correctly.

Initially, Microsoft Defender did not detect the records immediately. After waiting and checking again, DKIM was successfully enabled for:

    kozika.online

### Result

    DKIM: Enabled

---
<img width="1919" height="864" alt="image" src="https://github.com/user-attachments/assets/a71648be-8765-479a-a01b-a497e6b244be" />

# 3. DMARC Configuration

DMARC was already configured in Cloudflare.

Current record:

    v=DMARC1; p=none; rua=mailto:91d656de854d4a028f457a609a944537@dmarc-reports.cloudflare.net

### Current Policy

    p=none

This means DMARC is currently being used in monitoring mode.

The organization can collect reports and analyze authentication results before moving to a stronger enforcement policy.

### Result

    DMARC: Configured

---

# 4. Message Trace

Message Trace was used to investigate Exchange Online mail delivery.

We created a trace using:

    Sender:
    ahmedhassan@kozika.online

The trace showed different delivery states, including:

- Delivered
- Pending
<img width="1917" height="871" alt="image" src="https://github.com/user-attachments/assets/edf66b9b-ec60-4717-b4c0-59dfa6f071ca" />

---

# 5. Mail Delivery Troubleshooting Scenario

One message appeared as:

    Pending

The message details showed:

    Received
    Processed
    Not yet delivered

The important evidence was found in the Message Events.

The event showed:

    450 4.4.312 DNS query failed

It also showed:

    InfoNoRecords

And:

    FQDN=gmaul.com

The recipient address was:

    ahassanmm6@gmaul.com

The problem was that the domain was typed incorrectly.

The correct domain was:

    gmail.com

### Troubleshooting Process

#### Problem

The message was pending and had not been delivered.

#### Evidence

Message Trace showed:

    450 4.4.312 DNS query failed

#### Investigation

The destination FQDN was:

    gmaul.com

#### Finding

The recipient domain was incorrect.

#### Fix

The email was sent again to:

    ahassanmm6@gmail.com

#### Verification

The corrected message was successfully delivered.

### Troubleshooting Method

The scenario followed this process:

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

This is an important troubleshooting method for Exchange Administrators.
<img width="748" height="799" alt="image" src="https://github.com/user-attachments/assets/76dea71d-2c81-4e26-b6a9-b696b2e13db2" />

---

# 6. Mail Flow Rule

A Mail Flow Rule was created to identify messages coming from outside the organization.

### Rule Name

    External Email Warning

### Condition

    The sender is located outside the organization

### Action

    Prepend the subject of the message with [EXTERNAL]

The final rule was configured in:

    Enforce

### Purpose

The rule helps users identify external messages.

For example:

Original subject:

    External Test

After the rule:

    [EXTERNAL] External Test
<img width="1915" height="877" alt="image" src="https://github.com/user-attachments/assets/4641c036-617e-4eaf-bf5c-f08d8d4dd5ce" />

---

# 7. Mail Flow Rule Testing

An external message was sent to:

    ahmedhassan@kozika.online

The original subject was:

    External Test

After Exchange Online processed the message, the subject became:

    [EXTERNAL] External Test

The message was successfully delivered to the external mailbox.

### Result

The Mail Flow Rule was successfully applied.

---<img width="1889" height="834" alt="image" src="https://github.com/user-attachments/assets/ea44a599-2214-4663-8b01-483c95e3a576" />


# 8. Message Trace and Rule Troubleshooting

Message Trace was used to investigate mail flow behavior.

One important lesson from the test was that Message Trace data may not appear immediately after sending a message.

Recent messages can take some time before they become available in Message Trace.

Therefore, when troubleshooting a very recent message:

1. Wait for the message trace data to become available.
2. Run the trace again.
3. Check the message status.
4. Open the message details.
5. Review Message Events.
6. Identify the actual reason before making changes.

---

# 9. Final Configuration

The final Exchange Online mail authentication and mail flow configuration is:

| Component | Status |
|---|---|
| SPF | Configured |
| DKIM | Enabled |
| DMARC | Configured with `p=none` |
| Message Trace | Tested |
| Mail Flow Troubleshooting | Tested |
| External Email Warning Rule | Configured |
| External Email Warning Test | Successful |

---

# 10. Key Skills Practiced

This task provided practical experience with:

- Exchange Online mail flow
- SPF
- DKIM
- DMARC
- Cloudflare DNS
- Message Trace
- DNS troubleshooting
- Mail Flow Rules
- External email identification
- Reading Exchange delivery events
- Troubleshooting SMTP temporary errors
- Evidence-based troubleshooting

---

# 11. Troubleshooting Lessons

Important lessons from this task:

### Do not assume that Pending means a permanent failure

A message can be temporarily delayed while Exchange Online retries delivery.

### Always check Message Events

The message status alone may not explain the problem.

### Check the destination domain

A simple typo in an email address can cause DNS resolution failures.

### Use evidence before changing configuration

The Message Trace showed:

    450 4.4.312 DNS query failed

This provided enough evidence to investigate the destination domain instead of changing Exchange configuration.

### Test Mail Flow Rules before using them in production

A wrong transport rule can affect many messages.

Testing should be performed before applying a rule broadly.

---

# 12. Task Result

Task 05 - Exchange Mail Flow & Troubleshooting

Status: COMPLETED

The lab successfully demonstrated Exchange Online authentication, mail flow monitoring, troubleshooting, and Mail Flow Rule configuration.
