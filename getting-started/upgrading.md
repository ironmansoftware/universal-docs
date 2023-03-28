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

PowerShell Universal uses a script-based configuration system alongside a database used for retention of entities such as app tokens, job history and identities. If possible, you will want to backup these items before running an upgrade for easy rollback in case an issue is encountered during validation.&#x20;

### Database&#x20;

Backing up the database ensures that all apptokens, job history, identities and database secrets are retained in the case of an upgrade failure. SQL databases also may adjust the schema of the database and may require a rollback of not only the data, but also the schema of the tables in the database.&#x20;

#### LiteDB

By default, PowerShell Universal uses a single file database called LiteDB. Unless configured otherwise, the database is stored in `%ProgramData%\UniversalAutomation`. You should have a `database.db` and possibility a `database-log.db`. Both of these files should be backed up. The service must be stopped in order to backup the files.&#x20;

#### SQL

When using SQL for persistence, backup the entire database (including schema). There isn't necessarily a need to stop the PowerShell Universal service when backing up the database but it may continue to write to the database (for example when running scheduled jobs) after the backup has been completed.&#x20;

### Configuration Scripts

Scripts make up the main configuration data to backup when upgrading a production PowerShell Universal instance. For production, we recommend using a version control system. You can also take advantage of the built-in git integration. If you are using a two-way sync for PowerShell Universal git integration, consider tagging your git branch prior to the upgrade to allow for easy rollback to unexpected changes within the git repository.&#x20;

## 2. Upgrade Progress

Below are sections for each type of system upgrade and the steps that you should take based on how you originally installed PSU.&#x20;

### MSI

When installing via the MSI, you will want to follow the same backup procedures above.&#x20;

#### appsettings.json

You will want to back up the `appsettings.json` file stored in `%ProgramData%\PowerShellUniversal`. This file contains information such as port, data storage location and other server settings. Typically, the MSI will not make changes to this file once created. It will use the settings found for the upgraded version. That said, if necessary, the MSI will make changes to the appsettings file. These changes are considered breaking and will be listed in the changelog for the release.&#x20;

#### Service Account

When running an MSI upgrade, the PSU service is not uninstalled, and thus, the service account will still be set once the service starts up.&#x20;

{% hint style="info" %}
If you perform an uninstall and then an install using the MSI, then the service account will be removed.&#x20;
{% endhint %}

#### Upgrade Process

Once all the configuration files and the database are backed up, you can run the new MSI installer. The installer may prompt for a restart of the machine if files are locked. The PSU MSI will uninstall all the files in the installation directory and install entirely new files.&#x20;

Once the MSI has completed, you can navigate to your PowerShell Universal admin console to perform installation validation.&#x20;

### IIS

Below you will find information about upgrading an IIS install.&#x20;

#### web.config

In addition to the files listed to backup above, you will also want to consider backing up your `web.config` file. If you have made no changes to this file, you do not need to back it up.

The `web.config` file that is included in the application installation directory will be overwritten during upgrades. If you have moved your web.config file to an alternate location, it will not be overwritten. When creating an IIS website, you can simply include the `web.config` file in the web app's directory and have the [binaries stored in a different location](../config/hosting/hosting-iis.md).

#### Upgrade Process

When upgrading with IIS, you will need to first stop your application pool to ensure that the binaries used by IIS are no longer in use and then replace the binaries with the new ones. To ensure that the upgrade works as expected, it's recommended to delete all the application files and then unzip the new ones into the same directory to avoid assembly conflicts.&#x20;

{% hint style="info" %}
As with any installation from a ZIP file, make sure that you run `Get-ChildItem -Recurse | Unblock-File` from an elevated command prompt across the PowerShell Universal files to ensure they can be executed properly.&#x20;
{% endhint %}

Once you have copied the new files and unblocked them, start the app pool, navigate to the PowerShell Universal Admin Console and perform installation validation.&#x20;

### Universal Module

The Universal module can be used to upgrade installations of PowerShell Universal previously installed by the module.&#x20;

{% hint style="warning" %}
Do not use the Universal module to upgrade instances installed via MSI.&#x20;
{% endhint %}

Follow the backup procedures above and then perform the upgrade.&#x20;

First, upgrade the local PowerShell Universal module and verify the expected version is installed.&#x20;

```powershell
Update-Module Universal
Import-Module Universal -PassThru
```

Next, run `Update-PSUServer` to download and unzip the new PSU instance.&#x20;

```powershell
Update-PSUServer
```

After the upgrade is complete, navigate to the PowerShell Universal Admin Console and begin upgrade validation.&#x20;

### ZIP

Perform the necessary backup procedures and download the latest ZIP of PowerShell Universal.&#x20;

Stop the PowerShell Universal service. Delete the existing PowerShell Universal application files. Extract the ZIP files to the same directory. Finally, run `Unblock-File` against the directory to ensure that PSU can execute properly. Always run this command as administrator.&#x20;

```powershell
Get-ChildItem -Recurse | Unblock-File
```

After the upgrade is complete, navigate to the PowerShell Universal Admin Console and begin upgrade validation.&#x20;

## 3. Upgrade Validation

After running an upgrade, you should perform basic validation against your PSU server to ensure that it is fully functional.&#x20;

### Notifications

Verify that there are no errors within the notification drop down. They may be a sign of issues during the upgrade.&#x20;

### Environments

Verify that all environments are listed in the Settings \ Environments page. Although upgrades may not necessarily cause a change in environments, restarting the PowerShell Universal service (without an `environments.ps1` file) will cause PSU to rediscover environments. Updates to PowerShell outside of PSU may cause issues with PSU after it restarts.&#x20;

### Modules

Upgrades to PowerShell Universal may change assembly versions of DLLs shipped with the platform. This can cause other modules to fail to load. While this may not be obvious at first, you may consider taking an inventory of modules used in your platform to ensure that the versions are consistent before and after the upgrade to limit changes.&#x20;

If you have installed a version of the `Universal` module outside of PowerShell Universal (for example, with `Install-Module`), you must make sure to update the module or it can conflict with the new one installed with PowerShell Universal.&#x20;

### Dashboards

The most common upgrade issues come due to changes in the dashboard framework. Dashboards can be complex and bug fixes or features can sometimes cause for certain user's dashboards while fixing issues pertaining to another user's dashboard. Please read the changelog before upgrading to understand the impact of changes made to the dashboard framework and consider testing the dashboard with development data before upgrading in production.&#x20;

## Common Upgrade Issues

### IIS App Pool Does Not Start After Upgrade

The most common upgrade issue is that `Unblock-File` is not called properly on the extracted files when performing an upgrade of a IIS ZIP install. Also make sure to run the `Unblock-File` command recursively and from within an administrative session.&#x20;

Another command issue is extracting the files over the top of the existing files. This can cause assembly conflicts and puts the application in an unknown state. Follow the IIS upgrade documentation and delete the files before extracting them.&#x20;

### Command Not Found Errors

When new functionality is added to PowerShell Universal it is typically done using new cmdlets. If older versions of the PowerShell Universal module are installed on the system, it can cause conflicts with the one shipped within the installation media. Ensure that you have removed older versions of the `Universal` module if you encounter these errors.&#x20;

### Table\Column Not Found Error when using SQL Persistence

This can happen if SQL schema upgrades are not being run during upgrades. If you set the `RunMigrations` setting to `false` in `appsettings.json`, you must run the migrations manually or the PowerShell Universal service will not function properly.&#x20;

### Breaking Dashboard Component Change

These changes can be visual or functional. Please ensure that you review the changelog for items that may be related to the change you are seeing. Consider posting the forums or opening a GitHub issue to see if the issue is as designed and if there is a viable workaround.&#x20;

{% hint style="info" %}
We make the best possible effort to support everyone's' dashboards without breaking changes. That said, every configuration is pretty unique so we are more than happy to address issues you may encounter. Please, just let us know.&#x20;
{% endhint %}

### License Issues after Upgrade

The licensing model of PowerShell Universal provides licensed users the ability to upgrade to whatever is the newest version as long as they have an active perpetual or subscription license. If you attempt to upgrade a server that is no longer within the license window, the server will not function as expected. You will need to downgrade back to the previous version to restore functionality.&#x20;

Additionally, you may encounter issues due to the PSU service restart. When the service starts, it verifies license subscription status. If it fails to do so, it may not be licensed properly and cause other issues. The root cause is typically networking issues while attempting to access the IronmanSoftware.com website for activation. Offline license keys do not contact the IMS website for activation and will not encounter this issue.&#x20;

## 3.0 Breaking Changes

If you are upgrading from 2.x, you will have a couple of breaking changes.&#x20;

### Secret Variables Not Directly Defined

For performance reasons, secret variables are no longer automatically included in environments. To use secret variables, use the new [secret scope](../platform/variables.md#secret-scope).

### UD v2 Framework Removed

The UDv2 framework has been removed and is no longer supported. If you wish to use this framework, you can install it from the PowerShell Gallery.&#x20;

### IIS Hosting Package

If you are hosting in IIS, ensure that you install the [.NET 6.0 hosting bundle](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-6.0.3-windows-hosting-bundle-installer).&#x20;

### PowerShell Support

PowerShell 7.2 or later is supported by PowerShell Universal v3.&#x20;

## Migrating from LiteDB to SQL

In the PowerShell Universal installation directory, there you will find the [DataMigrator.exe](../config/persistence.md#data-migration) tool for moving data from a local LiteDB database to a SQL server database. It takes care of creating the dashboard, creating the schema and transferring data.&#x20;

{% hint style="info" %}
Although we only read data from LiteDB, we recommend backing it up before running the tool.&#x20;
{% endhint %}

Once migrated, you will need to update the plugin setting within `appsettings.json`. Replace the `UniversalAutomation.LiteDBv5` value with the string `SQL`. You can also set an environment variable to use the SQL plugin.&#x20;

```powershell
$ENV:Plugins__0 = "SQL"
```

You'll also need to replace the connection string value with your SQL Data \ ConnectionString.&#x20;

Similar to the plugin, you can use an environment variable instead of updating `appsetings.json`.

```powershell
$Env:Data__ConnectionString = "Data Source=ServerName; Initial Catalog=DatabaseName; User Id=UserName; Password=UserPassword;"
```

The step by step process is as follows:

1. Stop the PowerShell Universal service
2. Backup the database and repository
3. Run the data migration tool&#x20;
4. Update the appsettings.json or environment variable to enable the SQL plugin and set the connection string.&#x20;
5. Start the PowerShell Universal service

Once the service starts, it will be connected to SQL. Job data, identities, computers, and terminal instances will be stored in SQL.&#x20;

{% hint style="info" %}
If you are encountering issues with upgrades, you can use the `--ContinueOnError` flag to continue processing data even if an error is encountered. Typically, errors are the result of job history that may be missing a referential entity. LiteDB is document based while SQL is a relational database so some data may not translate perfectly.
{% endhint %}

