---
description: Changelog for PowerShell Universal.
---

# Changelog

## 5.0.0 - 8/20/2024

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

