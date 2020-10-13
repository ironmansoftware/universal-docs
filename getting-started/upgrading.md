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

The `web.config` file that is included in the application installation directory will be overwritten during upgrades. If you have moved your web.config file to an alternate location, it will not be overwritten. When creating an IIS website, you can simply include the `web.config` file in the web app's directory and have the [binaries stored in a different location](../config/hosting-iis/). 

#### Dashboard Components and Frameworks

New versions of Universal may include new versions of Universal Dashboard Frameworks or Components. By default, these components and frameworks are deployed to `%ProgramData%\PowerShellUniversal` during startup of the Universal server. During an upgrade, these files are not deleted. This ensures that dashboards will continue to run on the previous dashboard framework and component versions. 

You will have to manually upgrade your dashboards to use the new framework after the installation is complete. 

You should have multiple versions of the dashboard frameworks and components available when you start the new version of Universal. 

{% hint style="warning" %}
Note that if you are using nightly builds that the dashboard framework version may not change. This means you may not see changes if you have installed previous versions of a nightly build. You can delete the %ProgramData%\PowerShellUniversal folder to ensure that the most recent version of the dashboard framework is deployed. 
{% endhint %}

## ZIP Upgrade

When upgrading an manual ZIP file installation, you will need to stop the application, delete the entire binary folder and replace it with the new binary folder. When you start the new version of Universal, new dashboard frameworks and components will be deployed and the existing database will be loaded. 

## MSI Upgrade

To upgrade using the MSI, you can simply run the new version of the MSI. The MSI is setup to always perform a major upgrade. This means it will stop and remove the service, delete the entire installation directory, reinstall with the new files and then install and start the new service. 

You will want to follow the guide on data and configuration persistence above to ensure all your settings are saved. 

## IIS Upgrade

When upgrading with IIS, you will need to first stop your application pool to ensure that the binaries used by IIS are no longer in use and then replace the binaries with the new ones. Ensure that you follow the configuration persistence recommendations above with regards to the web.config file. 

