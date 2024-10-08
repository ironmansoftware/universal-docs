---
description: Local accounts in PowerShell Universal.
---

# Local Accounts

## Local Accounts

Local accounts are created and stored in the PowerShell Universal database. By default, credentials are stored in the local database vault.

To create a local account, you can navigate to Security \ Identities and create a new identity. Ensure that the Local Account switch is enabled and set a password.

<figure><img src="../.gitbook/assets/image (323).png" alt=""><figcaption></figcaption></figure>

If you have a licensed instance of PowerShell Universal, you can use a different credential vault.

## Admin Account

When first running PowerShell Universal, you will be prompted to set the admin account name and password.&#x20;

You can automate this by setting the following environment variables. The account will be created and assigned the Administrator role. Password restrictions are not enforced when using the environment variable.

```powershell
$ENV:PSUDefaultAdminPassword = "MyPassword"
$ENV:PSUDefaultAdminName = 'MyAdmin'
```

## Reset Admin Account

You can reset the admin account by specifying the `ResetAdminAccount` environment variable to `true` and then restarting the PowerShell Universal service. Ensure that the environment variable is set at the system level so that service has access to it. If no `admin` user is present, it will create one and set the password to `admin`. If one is present, it will reset the password to `admin`.&#x20;

## Password Restrictions

Passwords are required to be of at least 12 characters long and require a letter, number and symbol. Passwords will expire after 90 days. Users can reset their passwords at any time in the admin console or portal.&#x20;
