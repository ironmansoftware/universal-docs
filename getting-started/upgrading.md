---
description: This document covers upgrading the PowerShell Universal application.
---

# Upgrading

## Overview

This document will cover the upgrade process for production PowerShell Universal instances. We will cover the following topics.

1. Data Backup
2. Upgrade Process
3. Upgrade Validation

The Universal application binaries can generally be upgraded without having to change the configuration or database manually, but we do recommend backups of production data.

## 1. Data Backup

PowerShell Universal uses a script-based configuration system alongside a database used for retention of entities such as app tokens, job history and identities. If possible, you will want to backup these items before running an upgrade for easy rollback in case an issue is encountered during validation.

### Database

Backing up the database ensures that all apptokens, job history, identities and database secrets are retained in the case of an upgrade failure. SQL databases also may adjust the schema of the database and may require a rollback of not only the data, but also the schema of the tables in the database.

#### SQLite

By default, PowerShell Universal uses a single file database called SQLite. Unless configured otherwise, the database is stored in `%ProgramData%\UniversalAutomation`. You should have a `database.db` and possibility a `database-log.db`. Both of these files should be backed up. The service must be stopped in order to back up the files.

#### SQL

When using SQL for persistence, backup the entire database (including schema). There isn't necessarily a need to stop the PowerShell Universal service when backing up the database, but it may continue to write to the database (for example when running scheduled jobs) after the backup has been completed.

### Configuration Scripts

Scripts make up the main configuration data to backup when upgrading a production PowerShell Universal instance. For production, we recommend using a version control system. You can also take advantage of the built-in git integration. If you are using a two-way sync for PowerShell Universal git integration, consider tagging your git branch prior to the upgrade to allow for easy rollback to unexpected changes within the git repository.

## 2. Upgrade Progress

Below are sections for each type of system upgrade and the steps that you should take based on how you originally installed PSU.

### MSI

When installing via the MSI, you will want to follow the same backup procedures above.

#### appsettings.json

You will want to back up the `appsettings.json` file stored in `%ProgramData%\PowerShellUniversal`. This file contains information such as port, data storage location and other server settings. Typically, the MSI will not make changes to this file once created. It will use the settings found for the upgraded version. That said, if necessary, the MSI will make changes to the appsettings file. These changes are considered breaking and will be listed in the changelog for the release.

#### Service Account

When running an MSI upgrade, the PSU service is not uninstalled, and thus, the service account will still be set once the service starts up.

{% hint style="info" %}
If you perform an uninstall and then an install using the MSI, then the service account will be removed.
{% endhint %}

#### Upgrade Process

Once all the configuration files and the database are backed up, you can run the new MSI installer. The installer may prompt for a restart of the machine if files are locked. The PSU MSI will uninstall all the files in the installation directory and install entirely new files.

Once the MSI has completed, you can navigate to your PowerShell Universal admin console to perform installation validation.

### IIS

Below you will find information about upgrading an IIS install.

#### web.config

In addition to the files listed to backup above, you will also want to consider backing up your `web.config` file. If you have made no changes to this file, you do not need to back it up.

The `web.config` file that is included in the application installation directory will be overwritten during upgrades. If you have moved your web.config file to an alternate location, it will not be overwritten. When creating an IIS website, you can simply include the `web.config` file in the web app's directory and have the [binaries stored in a different location](../config/hosting/hosting-iis.md).

#### Upgrade Process

When upgrading with IIS, you will need to first stop your application pool to ensure that the binaries used by IIS are no longer in use and then replace the binaries with the new ones. To ensure that the upgrade works as expected, it's recommended to delete all the application files and then unzip the new ones into the same directory to avoid assembly conflicts.

{% hint style="info" %}
As with any installation from a ZIP file, make sure that you run `Get-ChildItem -Recurse | Unblock-File` from an elevated command prompt across the PowerShell Universal files to ensure they can be executed properly.
{% endhint %}

Once you have copied the new files and unblocked them, start the app pool, navigate to the PowerShell Universal Admin Console and perform installation validation.

### Universal Module

The Universal module can be used to upgrade installations of PowerShell Universal previously installed by the module.

{% hint style="warning" %}
Do not use the Universal module to upgrade instances installed via MSI.
{% endhint %}

Follow the backup procedures above and then perform the upgrade.

First, upgrade the local PowerShell Universal module and verify the expected version is installed.

```powershell
Update-Module Universal
Import-Module Universal -PassThru
```

Next, run `Update-PSUServer` to download and unzip the new PSU instance.

```powershell
Update-PSUServer
```

After the upgrade is complete, navigate to the PowerShell Universal Admin Console and begin upgrade validation.

### ZIP

Perform the necessary backup procedures and download the latest ZIP of PowerShell Universal.

Stop the PowerShell Universal service. Delete the existing PowerShell Universal application files. Extract the ZIP files to the same directory. Finally, run `Unblock-File` against the directory to ensure that PSU can execute properly. Always run this command as administrator.

```powershell
Get-ChildItem -Recurse | Unblock-File
```

After the upgrade is complete, navigate to the PowerShell Universal Admin Console and begin upgrade validation.

## 3. Upgrade Validation

After running an upgrade, you should perform basic validation against your PSU server to ensure that it is fully functional.

### Notifications

Verify that there are no errors within the notification drop down. They may be a sign of issues during the upgrade.

### Modules

Upgrades to PowerShell Universal may change assembly versions of DLLs shipped with the platform. This can cause other modules to fail to load. While this may not be obvious at first, you may consider taking an inventory of modules used in your platform to ensure that the versions are consistent before and after the upgrade to limit changes.

If you have installed a version of the `Universal` module outside of PowerShell Universal (for example, with `Install-Module`), you must make sure to update the module or it can conflict with the new one installed with PowerShell Universal.

### Apps

The most common upgrade issues come due to changes in the Universal App framework. Apps can be complex and bug fixes or features can sometimes cause for certain user's app while fixing issues pertaining to another user's app. Please read the changelog before upgrading to understand the impact of changes made to the app framework and consider testing the app with development data before upgrading in production.

## Common Upgrade Issues

### IIS App Pool Does Not Start After Upgrade

The most common upgrade issue is that `Unblock-File` is not called properly on the extracted files when performing an upgrade of a IIS ZIP install. Also make sure to run the `Unblock-File` command recursively and from within an administrative session.

Another command issue is extracting the files over the top of the existing files. This can cause assembly conflicts and puts the application in an unknown state. Follow the IIS upgrade documentation and delete the files before extracting them.

### Command Not Found Errors

When new functionality is added to PowerShell Universal it is typically done using new cmdlets. If older versions of the PowerShell Universal module are installed on the system, it can cause conflicts with the one shipped within the installation media. Ensure that you have removed older versions of the `Universal` module if you encounter these errors.

### Table\Column Not Found Error when using SQL Persistence

This can happen if SQL schema upgrades are not being run during upgrades. If you set the `RunMigrations` setting to `false` in `appsettings.json`, you must run the migrations manually or the PowerShell Universal service will not function properly.

### Breaking App Component Change

These changes can be visual or functional. Please ensure that you review the changelog for items that may be related to the change you are seeing. Consider posting the forums or opening a GitHub issue to see if the issue is as designed and if there is a viable workaround.

{% hint style="info" %}
We make the best possible effort to support everyone's' apps without breaking changes. That said, every configuration is pretty unique so we are more than happy to address issues you may encounter. Please, just let us know.
{% endhint %}

### License Issues after Upgrade

The licensing model of PowerShell Universal provides licensed users the ability to upgrade to whatever is the newest version as long as they have an active perpetual or subscription license. If you attempt to upgrade a server that is no longer within the license window, the server will not function as expected. You will need to downgrade back to the previous version to restore functionality.

Additionally, you may encounter issues due to the PSU service restart. When the service starts, it verifies license subscription status. If it fails to do so, it may not be licensed properly and cause other issues. The root cause is typically networking issues while attempting to access the IronmanSoftware.com website for activation. Offline license keys do not contact the IMS website for activation and will not encounter this issue.

## 5.0 Breaking Changes

### Removal of Pages

The drag and drop page designer has been removed in favor of [Portal Pages](../portal/portal-pages.md) and [Widgets](../portal/portal-widgets/).&#x20;

### Removal of App Pages Designer

The drag and drop page designer for apps has been removed. Apps created with the designer will still function.&#x20;

### Removal of Access Controls

Access Controls have been removed in favor of [Permissions](../security/enterprise-security/permissions.md). You can also use the [Portal ](broken-reference)to assign resources, like scripts, to users without the need for complicated permissions.&#x20;

### Cmdlet Communication Channel Change

Prior to v5, cmdlets would send data over HTTP or by using an internal gRPC channel. Now, all cmdlets use an externally facing gRPC Channel that is protected by authentication and authorization. It no longer uses standard REST API HTTP calls.&#x20;

This can be a problem for PowerShell Universal instances behind [reverse proxies](../config/hosting/reverse-proxy.md) and requires that the proper header values are sent.&#x20;

### PowerShell.exe is no longer used

The Windows PowerShell 5.1 environment no longer uses PowerShell.exe directly. It instead uses a .NET Framework version of the Universal.Agent.exe executable. This allows for the greatest compatibility with PowerShell Universal libraries and other modules. The agent still uses the PowerShell assemblies found on the executing machine.&#x20;

PowerShell.exe is no longer supported. It can be used in minimal environments.

### PowerShell 7 Environment No longer Uses Pwsh.exe

The default PowerShell 7 environment uses a .NET version of Universal.Agent.exe executable running PowerShell 7.4. This allows for the greatest compatibility with PowerShell Universal libraries and other modules.&#x20;

It's still possible to use the pwsh.exe process in custom environment configurations.&#x20;

### IIS Hosting Package

If you are hosting in IIS, ensure that you install the [.NET 8.0 hosting bundle](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-7.0.5-windows-hosting-bundle-installer).

### Integrated Environment PowerShell Version

The integrated environment now uses PowerShell 7.4.

### SQLite by Default

SQLite is the default persistence method. You will need to perform a manual conversion from LiteDB before installing version 5.

### LiteDB Support Removed

LiteDB has been removed as a supported database engine. Included with the PowerShell Universal installation files, you will find `psudb.exe`. It can be used to convert a LiteDB database into a SQLite database. Use the following command line.&#x20;

```powershell
.\psudb.exe -Path "$ENV:ProgramData\UniversalAutomation\database.db"
```

The tool will create a `database.bak` file before performing the conversion. Progress will be reported in the console.&#x20;

### Desktop Mode Removed

Desktop mode has been removed. Resources such as hot keys, file associations and shortcuts are no longer supported. The MSI now supports User scope installs that will run as the current user and start upon login.

### Install-PSUServer on Windows Installs from the MSI

In previous versions of PowerShell Universal, this command would install to a directory and create the service manually. This command now installs from MSI. If you previously installed with this module, you will need to remove the existing install with a previous version of the module and then install with the new version of the module.&#x20;

```powershell
Install-Module Universal -RequiredVersion 4.4.0
Remove-PSUServer
```

Open a new command prompt and run the following.&#x20;

```powershell
Uninstall-Module Universal
Install-Module Universal
Install-PSUServer
```
