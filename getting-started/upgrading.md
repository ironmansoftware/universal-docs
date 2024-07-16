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

#### LiteDB

By default, PowerShell Universal uses a single file database called LiteDB. Unless configured otherwise, the database is stored in `%ProgramData%\UniversalAutomation`. You should have a `database.db` and possibility a `database-log.db`. Both of these files should be backed up. The service must be stopped in order to backup the files.

#### SQL

When using SQL for persistence, backup the entire database (including schema). There isn't necessarily a need to stop the PowerShell Universal service when backing up the database but it may continue to write to the database (for example when running scheduled jobs) after the backup has been completed.

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

### Environments

Verify that all environments are listed in the Settings \ Environments page. Although upgrades may not necessarily cause a change in environments, restarting the PowerShell Universal service (without an `environments.ps1` file) will cause PSU to rediscover environments. Updates to PowerShell outside of PSU may cause issues with PSU after it restarts.

### Modules

Upgrades to PowerShell Universal may change assembly versions of DLLs shipped with the platform. This can cause other modules to fail to load. While this may not be obvious at first, you may consider taking an inventory of modules used in your platform to ensure that the versions are consistent before and after the upgrade to limit changes.

If you have installed a version of the `Universal` module outside of PowerShell Universal (for example, with `Install-Module`), you must make sure to update the module or it can conflict with the new one installed with PowerShell Universal.

### Dashboards

The most common upgrade issues come due to changes in the dashboard framework. Dashboards can be complex and bug fixes or features can sometimes cause for certain user's dashboards while fixing issues pertaining to another user's dashboard. Please read the changelog before upgrading to understand the impact of changes made to the dashboard framework and consider testing the dashboard with development data before upgrading in production.

## Common Upgrade Issues

### IIS App Pool Does Not Start After Upgrade

The most common upgrade issue is that `Unblock-File` is not called properly on the extracted files when performing an upgrade of a IIS ZIP install. Also make sure to run the `Unblock-File` command recursively and from within an administrative session.

Another command issue is extracting the files over the top of the existing files. This can cause assembly conflicts and puts the application in an unknown state. Follow the IIS upgrade documentation and delete the files before extracting them.

### Command Not Found Errors

When new functionality is added to PowerShell Universal it is typically done using new cmdlets. If older versions of the PowerShell Universal module are installed on the system, it can cause conflicts with the one shipped within the installation media. Ensure that you have removed older versions of the `Universal` module if you encounter these errors.

### Table\Column Not Found Error when using SQL Persistence

This can happen if SQL schema upgrades are not being run during upgrades. If you set the `RunMigrations` setting to `false` in `appsettings.json`, you must run the migrations manually or the PowerShell Universal service will not function properly.

### Breaking Dashboard Component Change

These changes can be visual or functional. Please ensure that you review the changelog for items that may be related to the change you are seeing. Consider posting the forums or opening a GitHub issue to see if the issue is as designed and if there is a viable workaround.

{% hint style="info" %}
We make the best possible effort to support everyone's' dashboards without breaking changes. That said, every configuration is pretty unique so we are more than happy to address issues you may encounter. Please, just let us know.
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

### IIS Hosting Package

If you are hosting in IIS, ensure that you install the [.NET 8.0 hosting bundle](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-7.0.5-windows-hosting-bundle-installer).

### Integrated Environment PowerShell Version

The integrated environment now uses PowerShell 7.4.

### SQLite by Default

SQLite is the default persistence method.&#x20;

### LiteDB Support Removed

LiteDB has been removed as a supported database engine.&#x20;
