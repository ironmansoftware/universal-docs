---
description: Changelog for PowerShell Universal.
---

# Changelog

## 5.0.6 - 9/9/2024

#### Admin Console

* Fixed an issue where the git pause switch wouldn't display the proper status when paused (#3688)
* Added delete computer button for offline computers (#3693)
* Improved display of charts on dashboard
* Fixed property label text wrapping in modal dialogs in the admin console (#3703)
* Improved admin portal page header formatting (#3704)
* Fixed an issue where the Discover Environments button would be enabled when git sync wasn't editing (#3714)
* Fixed an issue where editing git settings when using SQL would cause it to delete the settings (#3688)
* Fixed a display issue with the job feedback modal (#3692)
* Fixed the performance of the schedules page (#3659)
* Added missing Diagnostics button

#### APIs

* Fixed an issue calling Invoke-PSUScript in an unauthenticated API using the permissive security policy

#### Automation

* Fixed a SQLite locking issue when running many jobs at once
* Fixed an issue calling Invoke-PSUScript -Name with a path (#3708)

#### Apps

* Fixed an issue calling OnRender in OnRowExpand in New-UDTable (#3695)
* Fixed an issue calling Invoke-PSUScript in apps using the permissive security policy
* Fixed an issue with a base URL of / and the admin console routing (#3711)
* Fixed an issue where duplicate apps could show up after server restart (#3706)
* General fixes to Nivo Charts (#3682, #2083)

#### Platform

* Fixed an issue with redirect URL after login (#3694)
* Added support for configuring -TrustCertificate flag at the server level (#3697)
* Fixed an issue where variables stored in database would be null after restart (#3701)
* Removed 4MB limit for Universal cmdlet calls (#3700)
* Fixed an issue with psudb.exe where it could throw an exception attempting to move job output
* Fixed an issue with background job scheduling when using multi-node configurations
* Added -Migrate to psudb.exe to enabling migration to the newest schema in SQLite
* Fixed an issue where upgrades from v4 with New-PSUEnvironment -EnableDebugger would cause the environment to not show up (#3712)
* Fixed an issue where git sync would push even when there were no changes (#3713)

#### Portal

* Fixed an issue where an error could be displayed on the portal for certain authentication types

#### Security

* Updated .NET (8.0.8) and PowerShell (7.4.5) SDK versions to address security issues in dependencies
* Added missing View Claim Information button
* Fixed an issue enabling Anonymous Authentication and Windows Authentication in IIS (#3715)

## 5.0.5 - 9/3/2024

#### APIs

* Fixed an issue where endpoint content wouldn't be displayed in the admin console when using -Path
* Fixed an issue changing the path of endpoints (#3685)

#### Apps

* Fixed an issue where -DisableAutoStart had no affect (#3658)
* Fixed issue with -OnClick and -Theme on New-UDNivoChart (#3667)
* Added icon selector to page properties (#3678)
* Fixed an issue where a blank file and folder would be created if the app pointed to a path that didn't exist (#3679)
* Fixed an issue where installing apps from the library wouldn't show up (#3686)

#### Automation

* Added missing trigger schedule button

#### Platform

* Fixed an issue where the computer page would incorrectly show an error about the number of licensed computers.
* Fixed an issue where changing branding would duplicate lines in branding.ps1 (#3666)
* Fixed an issue with psudb.exe failing to convert jobs in certain configurations (#3670)
* Added permissive security model to cmdlets (#3676)
* Display number of selected changes in git commit (#3645)
* Fixed an issue where secret variable values would not be deleted from the database (#3654)
* Added missing clear cached claims button on the roles page.
* Fixed an issue running Connect-AzAccount

## 5.0.4 - 8/28/2024

#### Platform

* Fixed an issue loading custom health checks

#### Security

* ❗Fixed an issue where First Run dialog could be called multiple times

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

