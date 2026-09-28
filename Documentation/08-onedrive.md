# Task 08 - OneDrive for Business

## Objective

Configure and review OneDrive for Business administration settings.

The goal was to understand storage, retention, synchronization, notifications, and file-type restrictions.

## Environment

- Microsoft 365 Tenant: `kozika.online`
- OneDrive Administration: SharePoint Admin Center
- Default Storage Limit: 1024 GB
- Deleted User OneDrive Retention: 30 days

## 1. OneDrive Admin Settings

Reviewed:

**SharePoint Admin Center → Settings → OneDrive**

The following settings were available:

- Notifications
- Retention
- Storage limit
- Sync

## 2. Notifications

Current setting:

- Allow notifications about file activity: Enabled

Users can receive notifications about file activity and can turn off notifications if they do not want to receive them.

No change was required.

## 3. OneDrive Retention

Current setting:

- Deleted user OneDrive retention: 30 days

The setting controls how long a deleted user's OneDrive is retained.

The available range is:

- Minimum: 30 days
- Maximum: 3650 days

The default value of 30 days was kept for the lab.

## 4. Default Storage Limit

Current setting:

- 1024 GB

1024 GB equals 1 TB.

The setting defines the default OneDrive storage limit for qualifying licensed users.

A specific storage limit assigned to an individual user is not affected by changing the default value.

The default value was kept unchanged.

## 5. OneDrive Sync Settings

Reviewed the Sync administration settings.

Important options included:

- Limit syncing to specific domains
- Block uploads by file type
- OneDrive Sync application
- Sync troubleshooting

## 6. Block File Types

Configured a file-type restriction for OneDrive Sync.

Blocked extensions:

- `exe`
- `msi`
- `bat`
- `cmd`
- `ps1`

The extensions were entered without periods or spaces.

This policy is designed to prevent the specified file types from being uploaded through the OneDrive Sync client.
<img width="1919" height="936" alt="image" src="https://github.com/user-attachments/assets/2a844b24-f3a7-437d-88fe-6fda6cdf8f49" />



**Task 08 - OneDrive for Business: COMPLETED**

Skills practiced:

- OneDrive administration
- Storage management
- Deleted-user retention
- Sync administration
- File-type restrictions
- Policy scope
- Basic policy verification
