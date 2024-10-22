---
description: Migration from one PowerShell Universal server to another.
---

# Migration

It is often desirable to migrate a PowerShell Universal server configuration from one machine to another. This can be for operating system upgrades or general data center maintenance.&#x20;

This document explains the steps necessary to migrate PowerShell Universal to a new machine.&#x20;

We recommend stopping the PowerShell Universal service before performing the migration.&#x20;

```powershell
Stop-Service 'PowerShellUniversal'
```

## Configuration Data

The configuration data files are stored in `%ProgramData%\UniversalAutomation\Repository` by default. These will consist of features such as APIs, Scripts and Apps. The entire directory is necessary for the configuration of the new system to function.&#x20;

You can either copy the folder manually or via PowerShell. Ensure that you include all subdirectories.

```powershell
Copy-Item $ENV:ProgramData\UniversalAutomation\Repository \\newServer\C$\ProgramData\UniversalAutomation\Repository -Recurse
```

## Database

The database migration will depend on the type of database used.&#x20;

### SQLite&#x20;

You will need to copy the SQLite database file to the configured, or default, database location. On a default installation, this will be `%ProgramData%\UniversalAutomation\database.db`. The target machine account or service account will need read and write access to this database file.&#x20;

```powershell
Copy-Item $ENV:ProgramData\UniversalAutomation\database.db \\newServer\C$\ProgramData\UniversalAutomation\database.db 
```

### SQL and PostgreSQL

Because these databases are stored outside of the PowerShell Universal server, you do not need to perform a migration of the database itself. You will need to ensure that the target server has network access to the SQL host.&#x20;

## Application Settings

The PowerShell Universal `appsettings.json` file is necessary for providing the appropriate server settings to the platform. By default, this is stored in `%ProgramData%\PowerShellUniversal\appsettings.json`. You will need to copy this to the new server in the same location.&#x20;

This file contains configuration settings such as HTTP certificate, authentication, git sync settings, API configuration options and more.&#x20;

```powershell
Copy-Item $ENV:ProgramData\PowerShellUniversal\appsettings.json \\newServer\C$\ProgramData\PowerShellUniversal\appsettings.json 
```

## Secret Vaults

PowerShell Universal includes 3 built-in secret vaults that may need to be migrated. The database vault is included with the database migration and does not require extra steps.&#x20;

### PSUSecretStore&#x20;

The `PSUSecretStore` vault uses the Microsoft's [SecretStore module](https://learn.microsoft.com/en-us/powershell/utility-modules/secretmanagement/get-started/using-secretstore?view=ps-modules). This module stores secrets, on disk, using symmetric encryption. A default encryption key is included with PowerShell Universal installations. If the key was updated, the new key will be in the appsettings.json file you migrated in the previous step. You will also need to move the physical secret store to the new server's file system.&#x20;

The SecretStore module uses a user-specific storage location to ensure that ACLs are enforced on the files themselves. You will need to ensure that you copy the vault's contents to the account of the user that will be running PowerShell Universal on the new system.&#x20;

```powershell
Copy-Item $Env:LOCALAPPDATA\Microsoft\PowerShell\secretmanagement\localstore \\newServer\C$\Users\myServiceAccount\AppData\Local\Microsoft\PowerShell\secretmanagement\localstore 
```

### BuiltInLocalVault

The `BuiltInLocalVault` is only available on Windows and uses Credential Manager to store secrets. You will need to recreate these secrets in the Credential Manager store on the new system.&#x20;

Within Credential Manager, you will find PowerShell secrets stored with a `ps:` prefix.&#x20;

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

While it's not possible to extract credentials directly from the Credential Manager UI, you can use the Secret Management modules directly. To retrieve secrets, you can do the following.&#x20;

```powershell
Install-Module Micorosoft.PowerShell.SecretManagement
Install-Module SecretManagement.JustinGrote.CredMan
Register-SecretVault -Name 'BuiltInLocalVault' -ModuleName SecretManagement.JustinGrote.CredMan
Get-SecretInfo -Vault BuiltInLocalVault
$Secret = Get-Secret -Name 'TestApiKey' -Vault 'BuiltInLocalVault' -AsPlainText
```

On the new server, you can do the reverse and call `Set-Secret`. Note that these commands need to run as the service account running PowerShell Universal in order to store them properly in the Credential Manager account for the user.&#x20;

## Other Resources and Considerations

There may be other resources that PowerShell Universal uses on the system that should be taken into account when migrating servers.&#x20;

* PowerShell Modules&#x20;
* Environment Variables&#x20;
* Local Account Privileges
* File System Permissions&#x20;
* Proxy Configuration
* Certificates

## Application Files

Once all the following steps have been taken, you can now install PowerShell Universal on the new server.&#x20;

### MSI \ Kestrel&#x20;

The MSI package for PowerShell Universal installs the platform as a Windows service that hosts its own web server called Kestrel. To install the service, [download the MSI](https://powershelluniversal.com/downloads) and run it. We recommend using the exact same version as the source server.&#x20;

During the MSI install, leave all settings as default. We recommend leaving the service account blank and unchecking the box that states to start the PowerShell Universal service after the installation is complete.&#x20;

After the installation completes, the service will be created but not running. Open Service Control Manager (`services.msc`) and set the service account for the PowerShell Universal service. Start the service.&#x20;

## Debugging Issues

When migrating a PowerShell Universal service, you may run into issues the arise from configuration differences between the two systems. The following are places to look for more information.&#x20;

### Event Viewer

if the service starts and stops, there may be an issue with the database access. We recommend looking in the Application log within Event Viewer. PowerShell Universal will report two application Errors that will include .NET in the name. The second of the two errors will provide a human readable exception with more details.&#x20;

### System Logs

PowerShell Universal will write system logs to the %ProgramData%\PowerShellUniversal directory. Search for strings starting with `[ERR]` to gather more information about issues with the installation.&#x20;

### Notifications&#x20;

After migrating the service, check for any error notifications that may indicate misconfiguration of the system.&#x20;
