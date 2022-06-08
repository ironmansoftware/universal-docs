---
description: Changelog for PowerShell Universal.
---

# Changelog

## Changelog

## 3.0.0-rmt1 - 6/8/2022

### Added

* Support for notification levels (Information, Warning, Error)
* Added support for -OnRowExpand in New-UDTable
* Added support for Sync-UDElement against new New-UDTable
* Added support for any type in variable values
* Display build ID in the admin console
* Added PowerShell Protect integration
* Added support for hosting PowerShell Universal in a nested URL
* Added method selectors to the API endpoint page
* Added Copy published folder button
* Add Get-UDTheme and a default Ant Design theme

### Changed

* Settings and Login page scripts now use splatting when saving
* Fixed an issue where copy and paste would not work in terminals
* Fixed an issue where live logs would be blank
* Cleaned up the MSI installer to have better UX
* Identities now support assigning multiple roles
* PSU now locates all registered module repositories on the modules page
* Endpoints now check syntax before saving to endpoints.ps1
* Merge all fixes from 2.x



## 3.0.0-beta7 - 5/12/2022

### Added

#### Desktop

* Added support for triggering scripts on system events
* Hot key scripts will now receive a $HotKey parameter
* Added support for triggering scripts based on file associations
* Added support for triggering scripts based on custom protocols
* Added Show-PSUPage to display pages from the desktop client.

### Changed

#### Desktop

* Fixed an issue where you couldn't create hotkeys within the admin console.
* Fixed an issue where executing a hot key wouldn't work
* Fixed an issue where PowerShellUniversal.Desktop.exe was not included in the installer

#### Platform

* Fixed an issue where calling New-PSUSchedule from a dashboard wouldn't set the NextExecution time for a OneTime schedule

## 3.0.0-beta6 - 5/10/2022

### Added

#### APIs

* Added support for multiple API environments

#### User Interfaces

* Dashboards: Added dashboard templates to the create dashboard dialog.
* Dashboards: Added -Beat, -Fade, -BeatFade, and -Shake to New-UDIcon

### Changed

#### APIs

* Serialization depth is now set to 5
* ErrorAction now defaults to Stop

#### User Interfaces

* Dashboards: Fixed an issue where New-UDTransition would throw an error

#### Platform

* Fixed an issue where New-PSUScript wouldn't work within a dashboard
* Fixed an issue where Get-PSUCache wouldn't return cached items
* Fixed an issue where Get-PSUCache wouldn't unwind arrays
* Connect-PSUServer now returns information about the session after connection

## 3.0.0-beta4 - 4/21/2022

### ⚠️ Security Issue

* Fixed an issue where a user could access files outside of the published folder

### Changed

#### User Interfaces

* Dashboards: Fixed an issue where some icons would not show properly.

#### Automation

* Fixed an issue where time would be incorrect for jobs when using SQL storage

#### Platform

* Fixed an issue where Windows PowerShell modules would not be included in PSModulePath.
* Merged in latest v2.10 fixes

## 3.0.0-beta3 - 4/18/2022

### Changed

#### User Interfaces

* Dashboards: Fixed an issue where some icons would not show properly.

#### Automation

* Fixed an issue where time would be incorrect for jobs when using SQL storage

#### Platform

* Fixed an issue where Windows PowerShell modules would not be included in PSModulePath.
* Merged in latest v2.10 fixes

## 3.0.0-beta2 - 4/13/2022

### Changed

#### User Interfaces

* Dashboards: Fixed Find-UDIcon

#### Platform

* Fixed an issue where the database would not initialize properly
* Fixed an issue where the job log table would be inserted to rather than updated
* Fixed an issue where the computer name property would always be set to localhost for jobs
* Fixed an issue where the MSI installer would incorrectly set the SQL plugin

###

## 3.0.0-beta1 - 4/12/2022

### Removed

#### User Interfaces

* Dashboard: Removed UDv2 Framework
* Dashboard: Merged all components into the v3 framework.
* Removed UA aliases on PSU cmdlets
* Secret variables are no longer automatically included in environments

### Added

#### APIs

* Added support for multiple methods for an endpoint
* Added folder view for APIs
* Added Live Log view

#### User Interfaces

* Dashboards: Added New-UDStack
* Dashboards: Added -Schema to New-UDForm
* Dashboards: Added New-UDTimeline and New-UDTimelineItem
* Dashboards: Added New-UDBadge
* Dashboards: Added -Sx and -Component to New-UDStyle

#### Platform

* Added $Secret: scope for accessing secrets
* Added repository editor to edit all files in the repository.
* Added Settings \ General \ Diagnostics live log view
* Added Live Log view to Authentication and Authorization scripts.

### Changed

#### User Interfaces

* Dashboards: No longer deploy built in assets by default
* Dashboards: Reduced bundle size
* Dashboards: Updated to MUIv5
* Dashboards: Dashboard logs are now live

#### Platform

* Updated to .NET 6.0
* Added SQL server support for persistence
