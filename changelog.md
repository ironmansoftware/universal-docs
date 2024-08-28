---
description: Changelog for PowerShell Universal.
---

# Changelog

## 5.0.3 - 8/28/2024

#### Automation

* Fixed an issue displaying the scripts page

#### Apps

* Fixed a license expiration issue with data grids and date\time pickers

## 5.0.2 - 8/27/2024

#### Apps

* Fixed an issue with displaying non-authenticated apps (#3641)

#### Automation

* Fixed an issue with scheduling on Windows Server 2016 (#3647)
* Fixed an issue with script folder display (#3639, #3660)
* Fixed an issue where the Time Zone selector was missing for schedules (#3649)
* Added missing list view for scripts (#3635)
* Fixed an issue where the inline debugger wouldn't trigger in the integrated environment (#3622)
* Fixed an issue where schedule parameters would not display

#### Portal

* Fixed issue with parameter sets on the portal (#3617)

#### Platform

* Fixed issue with license enforcement in the admin console
* Fixed an issue where the agent would give up retrying to connect after some time (#3614)
* Fixed an issue with psudb.exe throwing an exception then migrating app tokens and jobs (#3652)
* Improved performance of psudb.exe
* Fixed an issue where disabling Windows Auth would cause users to fail to login until cookies were deleted (#3648)
* Fixed an issue where the platform would attempt to use powershell.exe, if configured
* Fixed an issue changing Script Base Path when API Base Path was already set (#3651)
* Fixed a locking issue with SQLite databases
* Fixed issue copying app tokens on HTTP servers (#3655)
* Improved connection logic in cmdlets to support more server configurations
* Fixed an issue with the online license activation retry failing

## 5.0.1 - 8/23/2024

#### APIs

* Fixed an issue when viewing endpoint documentation (#3607)
* Added event hub connections table
* Fixed an issue with Send-PSUEvent and -Parameters
* Fixed an issue with the endpoint tester and nested IIS sites (#3611)
* Added endpoint search (#3631)

#### Apps

* Fixed issues with the Pages tab in the app editor
* Live docs menu item now opens in a new tab
* Fixed an issue with New-UDTransferList (#3634)
* Fixed an issue with a New-UDDataGrid example

#### Automation

* Fixed an issue with job output appearing out of order

#### Platform

* Reduced the default System Log Level from Debug to Information
* Fixed an issue with environment discovery and Windows PowerShell 5.1
* Improved error reporting when jobs fail to start
* Fixed an issue with the configuration file editor (#3603)
* Fixed an issue with Universal cmdlets and HTTP
* Fixed an issue with SQLite v4 to v5 database update
* Fixed an issue logging in with SAML2 (#3623)
* Fixed an issue with home page formatting (#3620)
* Added select all button to the git commit page (#3584)
* Fixed a theme issue with the permission drawer (#3618)

## 5.0.0 - 8/20/2024

{% hint style="warning" %}
Please review the [upgrade documentation](getting-started/upgrading.md) before updating your environment.
{% endhint %}

#### Breaking Changes

* Removal of Pages
* Removal of Desktop mode
* Removal of App Designer
* Removal of LiteDB support

#### APIs

* Added endpoint tester
* Added support for string array query string parameters
* Added -ApiBaseFolder to Set-PSUSettings

#### Automation

* Added support for selecting streams when running a script manually
* Added Hide Run Later
* Added Quick Run button
* Added in-line debugger
* Extended job filtering to include all columns
* Added support for dynamic parameters
* Added -Tags to Invoke-PSUScript
* Added -HideChildren, -HideTriggered, -HideScheduled to Get-PSUJob&#x20;
* Added a page to view jobs for a schedule&#x20;
* JobRunId has been promoted from an experimental to a full feature
* Added support for script documentation

#### Apps

* Added -Path to Start-UDDownload
* Added -Sx to New-UDBadge&#x20;
* Added -RemoveMargin to New-UDCard
* Added -SelectedTabIndex to New-UDTabs
* Added -Enhanced to New-UDTransferList
* Added -DisableArcLinkLabels and -DisableArcLabels to New-UDNivoChart
* Added module support for apps

#### Portal

* Added preview version of Portal
* Added Portal Page designer
* Added Portal Widget editor&#x20;

#### Platform

* Added New Blazor-based Admin Console
* Updated to .NET 8.0 and PowerShell 7.4
* Added opt-in telemetry collection
* Get-PSUCache now returns the entire cache item information
* Added custom PSScriptAnalyzer rule to check for built in variable usage.
* Added a first run setup to set the default admin user name and password
* Added support for role-based access with PSUCache
* Added password complexity and expiration enforcement
* Added support for module variables
* Added Password and KeySize to appsettings.json to configure AES 256 database secrets
* Added stack traces to notifications
* Added support for Emoji favicons
* Added support for discovering Python environments
* Added PSUDefaultAdminPassword and PSUDefaultAdminName environment variables
* Added granular permissions throughout the platform
* Implemented gRPC cmdlets across the platform
* Added a process that checks for module updates
* Added a health check that verifies an environment exists
* Added tags for variables
* Added PostgreSQL Support
* Added Script Library
* Added an option for updating git submodules during a pull
* Added Pause Git Sync button
* Added configuration settings for the loading page
* Added a page to view all tagged resources&#x20;
* Added support for uploading to Published Folders
* Added support for database cache

