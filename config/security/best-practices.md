---
description: Security best practices for PowerShell Universal
---

# Best Practices

This document provides security best practices and hardening options for PowerShell Universal.&#x20;

## Authentication and Authorization

### App Token Enhanced Security

We recommend enabling app token enhanced security. App tokens generated within PowerShell Universal will be hashed and stored in the database rather than persisted in plaintext. As app tokens are used, they are hashed and compared against the hashed values. Tokens are hashed with SHA256.&#x20;

```powershell
Set-PSUSetting -EnhancedAppTokenSecurity
```

### App Token Signing Key

We recommend adjusting the default app token signing key. This setting is present in `appsettings.json`. Changing the signing key will invalidate existing app tokens.&#x20;

```json
"Jwt": {
    "SigningKey": "PleaseUseYourOwnSigningKeyHere"
}
```

### Authentication Configuration

Consider using `authentication.ps1` for configuring authentication methods that require secrets. When using authenticaiton.ps1, you can use secret variables and, in turn, secret vaults to load these values when starting up.&#x20;

```powershell
Set-PSUAuthenticationMethod -Type OIDC -ClientSecret $Secret:ClientSecret #...
```

### Default Admin Account

We recommend changing the default admin account password. By default, this password is stored within the PowerShell Universal database. You will receive a warning on the login page if the admin password is the default.&#x20;

### Default Authorization

Ensure that role scripts are either disabled or do not simply return true. Returning true from a role script will grant any user access to that role. With authentication methods like Windows Authentication, any user that is a capable of logging into the domain will have acecss to PowerShell Universal if the roles are not properly configured.&#x20;

```powershell
New-PSURole -Name 'Administrator' -Policy {
   # Grants administrator to everyone
   $true
}
```

### Least Privilged Access

Consider using a least privileged access model for roles within PowerShell Universal. Much of PowerShell Universal can be used with the execute or operator role. It isn't necessary to assign the administrator role to all users.&#x20;

### Limit Identities&#x20;

It may be desirable to limit identities to ones created within PowerShell Universal. This will prevent users from accessing PowerShell Universal if they have not been added on the identities page.&#x20;

```powershell
Set-PSUSetting -LimitIdentities
```

### Security Triggers

Consider creating triggers that will notify you of potential issues with authentication and authorization. The following triggers may be useful:&#x20;

* Revoked App Token Usage
* User Login
* New User Login&#x20;
* API Authentication Failed

## Automation

### Experimental Feature: Run ID

By default, job runs are stored as sequential big integers. This means that bad actors can guess job runs by incrementing a number from the current job ID. As of PowerShell Universal 3.8, an experimental feature can be enabled to only allow access of jobs by run ID. Run IDs are globally unique identifiers and cannot be guessed.&#x20;

```powershell
Set-PSUSetting -ExperimentalFeature @("JobRunId")
```

## Dashboards

### Avoid Long Running Event Handlers

Avoid running long running event handlers directly within dashboards. This can be an avenue for a denial-of-service attack. Consider running long running processes as jobs to take advantage of queuing.&#x20;

## Credentials and Secrets

### Secret Encryption Keys

If using the Database or PSUSecretStore vaults, we recommend changing the default passwords. Both systems use a symmetric encryption method for storing secrets. The Database secret stored encrypts values using the specified key into the database persistence layer. The PSUSecretStore creates a local file in the service account's profile with the secret values.&#x20;

```powershell
"Secrets": {
  "SecretStore": {
    "Password": "PSUSecretStore"
  },
  "Database": {
    "EncryptionKey": "=b0ywQA@VOSdr&R7an5g&XK6NVO%s4Tf"
  }
},
```

### Alternate Secret Storage

PowerShell Universal integrates with the Microsoft Secret Management module. This module provides the ability to interact with an extensible set of vaults. Many vault implementations can be found on the PowerShell Gallery.&#x20;

We recommend using a secure vault, such as Cyberark or Azure KeyVault, to store secrets in an enterprise ready fashion.&#x20;

Follow the documentation for [secret variable vaults](../../platform/variables.md) to learn how to configure an alternate vault.

## Service Configuration

### HTTPS&#x20;

Enabling HTTPS for the web server is highly recommended. If possible, we recommend storing a certificate within the Certificate Manager to avoid having to include a clear-text password for a local PFX file. Certificates are configured within `appsettings.json`.&#x20;

```json
{
  "Kestrel": {
    "Endpoints": {
      "HTTPS": {
         "Url": "https://*:443",
           "Certificate": {
             "Subject": "windows-server.ironman.local",
             "Store": "My",
             "Location": "LocalMachine",
             "AllowInvalid": "true"
           }
      }
   }
}
```

### Rate Limiting

Consider configuring rate limiting to avoid denial of service attacks. PowerShell Universal executes PowerShell in many different ways. PowerShell can be slower to execute than compiled languages so rate limiting can be very beneficial, especially for PowerShell Universal instances accessible externally.&#x20;

Learn more about [rate limiting here](best-practices.md#rate-limiting). &#x20;

### CORS Hosts

Consider configuring the CORS hosts setting in `appsettings.json` . You can learn more about the benefits of the [CORS hosts setting here](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS).&#x20;

```json
"CorsHosts": "",
```

### Service Accounts

Consider utilizing service accounts with a least-privileged access model. It's possible to configure the PowerShell Universal service to run as a service account that does not have access to certain resources and utilize alternate accounts when running scripts that need to access resources.&#x20;

Learn more about [service accounts here](../running-as-a-service-account.md).&#x20;

## Persistence

### SQL

We recommend the use of SQL server with integrated security or Azure managed identities. This avoids having to store passwords locally.&#x20;

### LiteDB

By default, the LiteDB database is not password protected. Actors that can physically access the PowerShell Universal server can copy the database file from disk and open it elsewhere. Consider providing an encryption key to the [LiteDB connection string to enable encryption](https://www.litedb.org/docs/connection-string/).

## Scripting

### PowerShell Security

PowerShell Universal exposes PowerShell scripts remotely in different ways. It's important to follow strict PowerShell script security best practices to guard against potentional attacks such as script injection.

Some recommendations include:

* Use of param blocks to validate input
* Avoiding Invoke-Expression to help prevent injection
* Code and security review processes on scripts

Learn more about [scripting security here](https://learn.microsoft.com/en-us/mem/configmgr/apps/deploy-use/learn-script-security).

### One-Way Git Sync

Consider using one-way git sync for changes in your production environment. This ensures that PowerShell Universal is read-only, and only validated changes will be picked up in production environments.&#x20;
