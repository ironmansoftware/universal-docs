---
description: This document covers upgrading the PowerShell Universal application.
---

# Upgrading

## General

The Universal application binaries can generally be upgraded without having to change the configuration or database manually. This document will cover how to upgrade the application and some caveats to be aware of in regards to configuration and data persistence.

### Data Persistence

Data is persisted in a LiteDB database with a default location of `%ProgramData%\UniversalAutomation\database.db`. The database will not be deleted during an upgrade of any kind. Any schema updates to the database will happen the first time you start up the new version of Universal. You may wish to backup your database before performing an upgrade.

### Configuration Persistence

Configuration files are stored by default in `%ProgramData%\UniversalAutomation`. Configuration files may be updated or transformed during an update. This will happen the first time that the new version of Universal server is started. You may wish to backup your configuration files before performing an upgrade.

If you are using git, changes to the Universal files will be synchronized after the server starts up.

#### appsettings.json

The `appsettings.json` file that is included in the application installation directory will be overwritten during upgrades. To avoid losing your settings in this file, consider installing it into the `%ProgramData%\PowerShellUniversal` folder. Universal will look at this folder first for [configuration settings. ](../config/settings.md#programdata-appsettings-json)

#### web.config

The `web.config` file that is included in the application installation directory will be overwritten during upgrades. If you have moved your web.config file to an alternate location, it will not be overwritten. When creating an IIS website, you can simply include the `web.config` file in the web app's directory and have the [binaries stored in a different location](../config/hosting/hosting-iis.md).

#### Dashboard Components and Frameworks

New versions of Universal may include new versions of Universal Dashboard Frameworks or Components. By default, these components and frameworks are deployed to `%ProgramData%\PowerShellUniversal` during startup of the Universal server. During an upgrade, these files are not deleted. This ensures that dashboards will continue to run on the previous dashboard framework and component versions.

You should have multiple versions of the dashboard frameworks and components available when you start the new version of Universal.

By default, new dashboards are set to always use the latest version of the dashboard framework. You can chose to set it to a specific version if you would like but will have to manually change the version during an upgrade.

**Repository**

Most of the settings for PowerShell Universal are stored within the repository folder. By default, this is in `%ProgramData%\UniversalAutomation\Repository`. While the upgrade should not affect these files, you may want to backup the files before upgrading.

## 3.0 Breaking Changes

If you are upgrading from 2.x, you will have a couple of breaking changes.&#x20;

### Secret Variables Not Directly Defined

For performance reasons, secret variables are no longer automatically included in environments. To use secret variables, use the new [secret scope](../platform/variables.md#secret-scope).

### UD v2 Framework Removed

The UDv2 framework has been removed and is no longer supported. If you wish to use this framework, you can install it from the PowerShell Gallery.&#x20;

### IIS Hosting Package

If you are hosting in IIS, ensure that you install the [.NET 6.0 hosting bundle](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-6.0.3-windows-hosting-bundle-installer).&#x20;

## PowerShell Upgrade

If you installed the platform using `Install-PSUServer`, you can use the `Update-PSUServer` cmdlet to upgrade the system.&#x20;

### Upgrade a Service

To upgrade a service, use `Update-PSUServer` and optionally specify the path to where the executable is stored.&#x20;

```
Update-PSUServer
```

### Upgrade an IIS Website

You can upgrade an IIS website by using the `-IISWebsite` parameter of `Update-PSUServer`.

```
Update-PSUServer -IISWebsite 'PSU'
```

## ZIP Upgrade

{% hint style="info" %}
Always ensure to run `Unblock-File` on Windows to unblock all the files extracted the ZIP. If you do not, PowerShell Universal will not function properly.
{% endhint %}

When upgrading an manual ZIP file installation, you will need to stop the application, delete the entire binary folder and replace it with the new binary folder. When you start the new version of Universal, new dashboard frameworks and components will be deployed and the existing database will be loaded.

## MSI Upgrade

To upgrade using the MSI, you can simply run the new version of the MSI. If you are upgrading from PowerShell Universal v2, you will need to uninstall and then upgrade to the new version.&#x20;

You will want to follow the guide on data and configuration persistence above to ensure all your settings are saved.



## IIS Upgrade

When upgrading with IIS, you will need to first stop your application pool to ensure that the binaries used by IIS are no longer in use and then replace the binaries with the new ones. Ensure that you follow the configuration persistence recommendations above with regards to the `web.config` file.

## Universal and UniversalDashboard Modules

When upgrading versions of PowerShell Universal, it is recommended to uninstall any previous versions of the `Universal` or `UniversalDashboard` modules you may have installed on the system. Having previous versions can cause problems with the PowerShell Universal server.&#x20;

To verify if you have previous versions installed, you can use the following command.&#x20;

```
Get-Module Universal -ListAvailable
Get-Module UniversalDashboard -ListAvailable
```

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

