---
description: Changelog for PowerShell Universal.
---

# Changelog

## Changelog

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
