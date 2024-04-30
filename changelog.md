---
description: Changelog for PowerShell Universal.
---

# Changelog

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
