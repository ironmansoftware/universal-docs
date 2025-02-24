---
description: Migrate or restore configuration of a PowerShell Universal system.
---

# Migrate and Restore

It is often desirable to migrate a PowerShell Universal server configuration from one machine to another. This can be due to change of infrastructure or restoring from backup. This can be for operating system upgrades or general data center maintenance.

This document explains the steps necessary to migrate PowerShell Universal configuration to another machine.

We recommend stopping the PowerShell Universal service before performing the migration or restore.

```powershell
Stop-Service 'PowerShellUniversal'
```

Depending on the type of migration or restoration, you may not need to perform all of these actions.

## Configuration Data

The configuration data files are stored in `%ProgramData%\UniversalAutomation\Repository` by default. These will consist of features such as APIs, Scripts and Apps. The entire directory is necessary for the configuration of the target system to function.

You can either copy the folder manually or via PowerShell. Ensure that you include all subdirectories.

```powershell
Copy-Item $ENV:ProgramData\UniversalAutomation\Repository \\newServer\C$\ProgramData\UniversalAutomation\Repository -Recurse
```

## Database

The database migration will depend on the type of database used.

### SQLite

You will need to copy the SQLite database file to the configured, or default, database location. On a default installation, this will be `%ProgramData%\UniversalAutomation\database.db`. The target machine account or service account will need read and write access to this database file.

```powershell
Copy-Item $ENV:ProgramData\UniversalAutomation\database.db \\newServer\C$\ProgramData\UniversalAutomation\database.db 
```

If you are restoring from backup, you may need to [Downgrade](downgrade.md) the schema if you upgraded the version.

### SQL and PostgreSQL

Because these databases are stored outside of the PowerShell Universal server, you do not need to perform a migration of the database itself. You will need to ensure that the target server has network access to the SQL host.

If you are restoring from backup, you may need to [Downgrade](downgrade.md) the schema if you upgraded the version.

## Application Settings

The PowerShell Universal `appsettings.json` file is necessary for providing the appropriate server settings to the platform. By default, this is stored in `%ProgramData%\PowerShellUniversal\appsettings.json`. You will need to copy this to the new server in the same location.

This file contains configuration settings such as HTTP certificate, authentication, git sync settings, API configuration options and more.

```powershell
Copy-Item $ENV:ProgramData\PowerShellUniversal\appsettings.json \\newServer\C$\ProgramData\PowerShellUniversal\appsettings.json 
```

appsettings.json files do not change between upgrades and you likely not need to perform this action during a restore.

## Secret Vaults

PowerShell Universal includes 3 built-in secret vaults that may need to be migrated. The database vault is included with the database migration and does not require extra steps. If you are performing a restore, it's unlikely you will need to perform these restore operations unless the secret vaults have become corrupted.

### PSUSecretStore

The `PSUSecretStore` vault uses the Microsoft's [SecretStore module](https://learn.microsoft.com/en-us/powershell/utility-modules/secretmanagement/get-started/using-secretstore?view=ps-modules). This module stores secrets, on disk, using symmetric encryption. A default encryption key is included with PowerShell Universal installations. If the key was updated, the new key will be in the appsettings.json file you migrated in the previous step. You will also need to move the physical secret store to the new server's file system.

The SecretStore module uses a user-specific storage location to ensure that ACLs are enforced on the files themselves. You will need to ensure that you copy the vault's contents to the account of the user that will be running PowerShell Universal on the new system.

```powershell
Copy-Item $Env:LOCALAPPDATA\Microsoft\PowerShell\secretmanagement\localstore \\newServer\C$\Users\myServiceAccount\AppData\Local\Microsoft\PowerShell\secretmanagement\localstore 
```

### BuiltInLocalVault

The `BuiltInLocalVault` is only available on Windows and uses Credential Manager to store secrets. You will need to recreate these secrets in the Credential Manager store on the new system.

Within Credential Manager, you will find PowerShell secrets stored with a `ps:` prefix.

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

While it's not possible to extract credentials directly from the Credential Manager UI, you can use the Secret Management modules directly. To retrieve secrets, you can do the following.

```powershell
Install-Module Micorosoft.PowerShell.SecretManagement
Install-Module SecretManagement.JustinGrote.CredMan
Register-SecretVault -Name 'BuiltInLocalVault' -ModuleName SecretManagement.JustinGrote.CredMan
Get-SecretInfo -Vault BuiltInLocalVault
$Secret = Get-Secret -Name 'TestApiKey' -Vault 'BuiltInLocalVault' -AsPlainText
```

On the new server, you can do the reverse and call `Set-Secret`. Note that these commands need to run as the service account running PowerShell Universal in order to store them properly in the Credential Manager account for the user.

## Authentication

Certain authentication types will require configuration outside of PowerShell Universal. Unless you are moving the machine running PowerShell Universal or changing the accessible URLs, you will not need to perform these actions.&#x20;

### OpenID Connect

Ensure that the proper sign-on URLs are configured in your Identity provider (e.g. Azure AD or Okta) if the host name of the server is changing. Without properly configured sign-on URLs, users will not be able to sign on the new system.

### Windows

[Windows authentication](../security/enterprise-security/windows-sso.md) requires the setup of an SPN for the service account running the PowerShell Universal service. Ensure this SPN is in place before attempting to use Windows authentication with the new system.

## Other Resources and Considerations

There may be other resources that PowerShell Universal uses on the system that should be taken into account when migrating or restoring servers. Typically, you will not need to worry about these resources during a restore as they should remain the same if the machine has not changed.

* PowerShell Modules
* Environment Variables
* Local Account Privileges
* File System Permissions
* Proxy Configuration
* Certificates
* Git SSH keys or credentials
* DNS Settings

## Application Files

Once all the following steps have been taken, you can now install PowerShell Universal on the new server. If you are downgrading during a restore, please follow the [Downgrade ](downgrade.md)documentation.

### MSI \ Kestrel

The MSI package for PowerShell Universal installs the platform as a Windows service that hosts its own web server called Kestrel. To install the service, [download the MSI](https://powershelluniversal.com/downloads) and run it. We recommend using the exact same version as the source server.

During the MSI install, leave all settings as default. We recommend leaving the service account blank and unchecking the box that states to start the PowerShell Universal service after the installation is complete.

After the installation completes, the service will be created but not running. Open Service Control Manager (`services.msc`) and set the service account for the PowerShell Universal service. Start the service.

## Debugging Issues

When migrating a PowerShell Universal service, you may run into issues the arise from configuration differences between the two systems. The following are places to look for more information.

### Event Viewer

if the service starts and stops, there may be an issue with the database access. We recommend looking in the Application log within Event Viewer. PowerShell Universal will report two application Errors that will include .NET in the name. The second of the two errors will provide a human readable exception with more details.

### System Logs

PowerShell Universal will write system logs to the %ProgramData%\PowerShellUniversal directory. Search for strings starting with `[ERR]` to gather more information about issues with the installation.

### Notifications

After migrating the service, check for any error notifications that may indicate misconfiguration of the system.
