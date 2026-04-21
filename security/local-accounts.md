---
description: Local accounts in PowerShell Universal.
---

# Local Accounts

## Local Accounts

Local accounts are created and stored in the PowerShell Universal database. By default, credentials are stored in the local database vault.

To create a local account, you can navigate to Security \ Identities and create a new identity. Ensure that the Local Account switch is enabled and set a password.

<figure><img src="../.gitbook/assets/image (211).png" alt=""><figcaption><p>Local Account Dialog</p></figcaption></figure>

If you have a licensed instance of PowerShell Universal, you can use a different credential vault.

## Admin Accounts

PowerShell Universal prompts you to configure the administrator account name and password the first time it runs, but this process can be automated by setting the PSUDefaultAdminName and PSUDefaultAdminPassword environment variables. When these variables are used, the account is created and assigned the Administrator role, and password restrictions are not enforced. If you become locked out of the server, you can reset the administrator account by setting the ResetAdminAccount environment variable to true and restarting the PowerShell Universal service. This variable must be defined at the system level so the service can access it. If no administrator account exists, PowerShell Universal will create one and set its password to admin; otherwise, it will reset the existing administrator account password to admin.

**PSUDefaultAdminName** - Specifies the name of the administrator account to create during initial setup.\
**PSUDefaultAdminPassword** - Specifies the password for the administrator account to create during initial setup.\
**ResetAdminAccount** - Resets the administrator account password to admin after the PowerShell Universal service is restarted, or creates a new administrator account with that password if one does not already exist.

```
$ENV:PSUDefaultAdminPassword = "MyPassword"
$ENV:PSUDefaultAdminName = 'MyAdmin'
```

## Password Restrictions

Passwords are required to be of at least 12 characters long and require a letter, number and symbol. Passwords will expire after 90 days. Users can reset their passwords at any time in the admin console or portal.
