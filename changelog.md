---
description: Changelog for PowerShell Universal.
---

# Changelog

## 5.0.0-rc1 - 7/16/2024

## Automation

* Fixed issue with parameters from scripts provided by modules
* Fixed issue with job filters on the Jobs page.

## Portal

* Added row and column guides to the Portal Page editor

## Platform

* Added a first run setup to set the default admin user name and password (#2616)
* Added support for role-based access with PSUCache (#2963)
* Fixed an issue using gRPC cmdlets in Apps
* Added password complexity enforcement
* Added password expiration enforcement

## 5.0.0-beta7 - 7/2/2024

## APIs

* Fixed an issue with connecting to event hubs

## Automation

* Added Pipeline Output Tab
* Jobs Run Today now links to a page that only shows jobs run today (#3321)

## Apps

* Added -Path to Start-UDDownload
* PowerShell Apps have been renamed back to Apps

## Platform

* Added support for module variables (#2711)
* Fixed an issue with IntelliSense
* Fixed an issue creating resources when git sync was enabled
* Fixed a SQLite database locking error
* Added Git Commit Discard button
* Enabled the file system watcher
* Fixed an issue with Windows PowerShell.
* Added Password and KeySize to appsettings.json to configure AES 256 database secrets (#3291)

## Portal

* Blazor Apps have been renamed to Portal Widgets and Pages
* Added support for properties in Portal Widgets

## 5.0.0-beta6 - 6/16/2024

#### Automation

* Fixed issue with creating schedules (#3361)
* Job status filters now persist refreshes (#3340)
* Fixed an issue with the Jobs Failed Today widget on the home page (#3391)
* Fixed an issue with script folders (#3398)

#### Platform

* Fixed an issue with Telemetry (#3347)
* Added health check refresh, run and clear buttons
* Fixed routing for nested sites
* Fixed an issue with the groom job when using PostreSQL (#3360)
* Fixed a login page redirect issue (#3366)
* Fixed an issue accessing the secret scope (#3372)
* Fixed an issue saving modules on non-Windows systems (#3371)
* Fixed issue with deleting a license
* Fixed an issue with file management when One-Way git sync was enabled (#3377)
* Fixed an issue with the Import command in the library when One-Way git sync is enabled (#3374)
* Fixed an issue with environment discovery (#3378)
* Fixed an issue with the module controller (#3390)
* Fixed issues with notification badge (#3387)
* Fixed an issue editing git settings when One-Way Git Sync was enabled (#3389)
* Fixed an issue with git settings validation (#3396)
* Fixed an issue with the file page's title (#3400)
* Added git commit file selector (#3403)
* Added live logging checkbox

#### Portal

* Added Display In Portal and Roles to tags
* Added grouping of resources by tags

#### Security

* Added input box for role default routes

## 5.0.0-beta5 - 5/22/2024

#### Automation

* Added filter output by stream to job page (#3298)
* Fixed syntax highlighting of job logs
* Added Hide Run Later
* Fixed an issue with Hide Run As, Hide Run On and Hide Environment settings
* Added Quick Run button for scripts (#3319)
* Added support for dynamic parameters (#2372)
* Added -Tags to Invoke-PSUScript (#3302)

#### Blazor Apps

* Fixed issue with authentication and roles settings

#### PowerShell Apps

* Fixed an issue with Get-UDPage

#### Platform

* Added My Identity page (#2862)
* Fixed some issues with the git edit button and commit page
* Fixed PowerShell IntelliSense
* Added stack traces to notifications
* Fixed an issue with Branding \ Admin Console Title
* Added support for Emoji favicons
* Fixed an issue with gRPC errors in some environments
* Added support for discovering Python environments
* Fixed an issue with PostgreSQL support
* Fixed an error adding git settings
* Added PSUDefaultAdminPassword and PSUDefaultAdminName

#### Portal

* Added Portal
* Added Portal link to admin console
* Added dashboard page
* Added Services page
* Added scripts to services page

## 5.0.0-beta4 - 5/6/2024

#### APIs

* Fixed an issue with the header tab on the API test page
* Fixed an issue with API Docs (#3311)

#### Automation

* Fixed an issue where error messages would be written twice in the output log (#3305)
* Fixed an issue with creating schedules.
* Fixed an issue with one-time schedules

#### Platform

* Added permission enforcement for all cmdlets
* Fixed an issue with OIDC authentication
* Fixed an issue with the default authentication warning being shown even when authentication was configured.
* Fixed an issue with the integrated security context for PSU cmdlets
* Reduced server start up time
* Fixed an issue logging in with demo mode
* Fixed an issue with New-PSUPublishedFolder
* Fixed a performance issue with the admin console

## 5.0.0-beta3 - 4/29/2024

### Automation

* Added inline script debugging terminal

### Platform

* Added granular permissions throughout the platform
* Added custom module editor
* Implemented gRPC cmdlets across the platform

## 5.0.0-beta2 - 4/10/2024

### API

* Added API Test Tab
* Added Invoke-PSUEndpoint

### Automation

* Added Terminals and Terminal History pages
* Added folders for scripts
* Added new columns to the jobs table

### Platform

* Added a process that checks for module updates
* Added a health check that verifies an environment exists
* Added tags for variables

## 5.0.0-beta1 - 3/11/2024

#### Major Features

* New Admin Console based on Blazor
* PostgreSQL support
* Blazor Apps
* Script Library

#### Breaking Changes

* PowerShell Universal defaults to SQLite
* PowerShell App designer has been removed
* LiteDB Support has been removed
* Removed support for pages
* Removed -Mask from New-UDTextbox

#### PowerShell Apps

* Added -Sx to New-UDBadge (#2878)
* Added -RemoveMargin to New-UDCard
* Added -SelectedTabIndex to New-UDTabs (#2897)
* Remove mandatory on text for New-UDMenuItem (#2906)
* Added -Enhanced to New-UDTransferList (#2888)
* Fix issue with New-UDAutocomplete always being fullwidth (#2949)
* Fix issue with New-UDTextbox date hand enter (#3006)
* Added -DisableArcLinkLabels and -DisableArcLabels to New-UDNivoChart (#2907)
* Fix issue with 'line' Chartjs issue (#2871)
* Added module support for apps (#2177)

#### APIs

* Added -ApiBaseFolder to Set-PSUSettings (#2794)

#### Automation

* Added -HideChildren, -HideTriggered, -HideScheduled to Get-PSUJob (#2444)
* Added a page to view jobs for a schedule (#1377)
* JobRunId has been promoted from an experimental to a full feature (#2799)
* Added support for script documentation (#2743)

#### Platform

* Added an option for updating git submodules during a pull (#2889)
* Computers and computer groups are now visible in single-node environments (#2915)
* Added Pause Git Sync button (#2994)
* Customize logged out page (#2643)
* Added configuration settings for the loading page
* Improved the access denied error for the CPU health check (#2671)
* Added support for customizing the table name for log entries in SQL and PostgreSQL (#2786)
* Added a page to view all tagged resources (#1302)
* Added support for uploading to Published Folders (#2555)
* Added support for database cache
