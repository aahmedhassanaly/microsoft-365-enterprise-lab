# Task 01 — Microsoft 365 Tenant & Organization Setup

## Objective

Set up the basic Microsoft 365 environment for the fictional company **Kozika Online** and prepare the tenant for the following Microsoft 365 infrastructure tasks.

The main goal was to review the tenant configuration and add the company's custom domain without connecting unnecessary services at this stage.

---

## Environment

- Microsoft 365
- Microsoft Entra ID
- Cloudflare DNS
- Custom Domain: `kozika.online`

---

## 1. Microsoft Entra ID Tenant Review

The Microsoft Entra ID overview was reviewed to confirm that the Microsoft 365 tenant was available and that the administrator account had the required administrative access.

The following information was verified:

- Microsoft Entra ID tenant exists
- Administrator account exists
- Global Administrator role is available
- Users and Groups are available
- Entra Connect is not configured
- No devices are currently registered for the lab

This confirms that the Microsoft 365 environment is ready for the lab.

---

## 2. Organization Information

The Microsoft 365 organization information was reviewed.

The default Microsoft 365 domain was:

`kozika12.onmicrosoft.com`

The organization information was kept simple because this is a training environment.

No unnecessary tenant-wide settings were changed.

---

## 3. Add Custom Domain

The custom company domain was added:

`kozika.online`

The domain is managed through **Cloudflare DNS**.

During the setup, Microsoft 365 provided two methods for connecting the domain:

1. Let Microsoft add the DNS records automatically
2. Add the DNS records manually

The manual option was selected.

### Reason

Using manual DNS management gives better control over the lab environment and allows the DNS configuration to be introduced when each Microsoft 365 service is required.

---

## 4. Microsoft 365 DNS Services

Microsoft 365 displayed DNS records for several services, including:

### Exchange Online

- MX
- TXT/SPF
- CNAME Autodiscover

### Basic Mobility & Security

- `enterpriseregistration` CNAME
- `enterpriseenrollment` CNAME

### DKIM

DKIM DNS records were also available under the advanced options.

These services were **not connected during this task**.

---

## 5. Service Configuration Decision

No Microsoft 365 services were selected during the domain connection stage.

The domain status showed:

`No services selected`

This is intentional.

The lab will configure each service in its appropriate task instead of enabling everything during the initial domain setup.

Planned service configuration:

| Service | Planned Task |
|---|---|
| Exchange Online | Task 04 |
| Exchange Mail Flow | Task 05 |
| Intune | Task 09 |
| Conditional Access | Task 12 |
| Defender | Task 13 |
| Purview | Task 14 |

---

## 6. Verification

The following items were verified:

- Microsoft 365 tenant is accessible
- Global Administrator access is available
- Organization information is accessible
- `kozika.online` was added to the tenant
- Cloudflare is the DNS hosting provider
- Manual DNS configuration was selected
- Microsoft 365 services were intentionally left unconnected
- No unnecessary DNS records were added

---

## Result

The basic Microsoft 365 tenant and organization setup is complete.

The custom domain `kozika.online` is registered in the Microsoft 365 environment, while Exchange, Intune, DKIM, and other services will be configured later as part of the lab.

This approach keeps the environment organized and allows each service to be configured and tested separately.


## Status

**COMPLETED**
<img width="1904" height="868" alt="image" src="https://github.com/user-attachments/assets/e23ccc39-8969-4a8a-8d37-dfac4061ff72" />
