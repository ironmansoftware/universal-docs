---
description: Changelog for the Visual Studio Code extension for PowerShell Universal.
---

# Extension Changelog

## 2.5.0 - 11/10/2021

* Added support for editing individual endpoints
* Removed settings for starting the PSU server from the extension.

## 2.3.0 - 9/14/2021

* Aligned PSU version with extension version&#x20;
* Fixed an issue where an error would be shown when loading the extension
* Fixed an issue where the wrong URL was used for viewing scripts

## 2.1.1 - 7/22/2021

* Fixed an issue with module updates
* Fixed an issue with Connect-PSUServer being called before modules were installed

## 2.1.0 - 7/22/2021

* Added support for view job status, logs, and pipeline output
* Force PowerShell extension to initialize when starting Universal
* Connect to the PowerShell Universal server (if configured) during startup

## 2.0.1 - 7/21/2021

* Fixed an issue where remote editing of dashboards would not work

## 2.0.0 - 7/20/2021

* Added 'Connect via Admin Console' to the connection dialog
* Added support for dashboard components and frameworks
* Added commands to install dashboard components and frameworks
* Added a check during startup for the current version of the Universal and UniversalDashboard modules
* Added a setting to disable the update module check (Check Modules)&#x20;
* Improved the error message generated when the extension fails to connect to the server
* Fixed an issue with the URL for viewing jobs
* Fixed an issue with the URL for viewing the admin console page
* Dropped support for Universal 1.5&#x20;

## 1.9.0 - 6/1/2021

* Added support for self configuration in PowerShell Universal v2

## 1.8.2 - 4/15/2021

* Fixed an issue where endpoints.ps1 and dashboards.ps1 could not be opened remotely

## 1.8.1 - 3/4/2021

* Fixed an issue where the Local Editing setting was on by default
* Added an error message when a local file isn't found

## 1.8.0 - 3/1/2021

* Added Local Editing Setting to edit files locally rather than via the REST API.&#x20;

## 1.7.5 - 2/25/2021

* Scripts are now sorted by name alphabetically
* An error is now shown when the extension cannot connect to PowerShell Universal&#x20;
* Removed the auto-import of UD and PSU modules. We recommend you install these from the PowerShell Gallery&#x20;

```
Install-Module Universal
Install-Module UniversalDashboard
```

## 1.7.4 - 1/21/2021

* Fixed an issue where the extension would fail to initialize on non-internet connected machines.&#x20;

## 1.7.3 - 12/31/2020

**Changed**

* Simplified first-time start up to attempt to connect with default settings to avoid having to do any configuration manually.&#x20;

## 1.7.2 - 12/30/2020

**Added**

* Settings for controlling the sample browser

**Changed**

* Improved the error message returned when attempting to automatically grant an app token and it fails.&#x20;

## 1.7.1 - 12/29/2020

### Added

* Added a Sample Browser for inserting samples from the PowerShell Universal Samples Repository

## 1.7.0 - 12/28/2020

{% hint style="warning" %}
Breaking Change: This version of the extension only works with version 1.5.0 or later of PowerShell Universal
{% endhint %}

**Added**

* Added a version check for notification there is a new version of Universal
* Added a URL setting for connecting to PowerShell Universal
* Added new connection workflow to make it easier and more clear on how to connect to Universal.

**Changed**

* The extension now uses the REST API to make changes to configuration scripts
* Deprecated the Port and Computer name settings in favor of the URL setting
* The extension no longer automatically downloads PowerShell Universal

## \[1.6.1]

### Changed

* Fixed issue when attempting to download on Windows or Mac
* Fixed issue where extension would not work with Mac OS X

## \[1.6.0]

### Added

* Added support for Debug-PSUDashboard

### Changed

* Replaced PowerShell Versions with Environments in the configuration tree view

## \[1.5.1]

### Changed

* Fixed an issue where the extension wouldn't activate correctly.

## \[1.5.0]

### Added

* Add a command for manually refreshing the PSU configuration

### Changed

* Fixed an issue where components wouldn't import correctly

## \[1.4.0]

### Added

* Added a setting to disable starting the PowerShell Universal server on extension activation.

### Changed

* Extension will fail to activate after a number of retries while connecting to the Universal server.

## \[1.3.0]

* Added support configuration files.&#x20;

## \[1.2.0]

* Added support for scripts and jobs.

## \[1.1.0]

* Added support for APIs

## \[1.0.0]

* Initial release
