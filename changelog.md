---
description: Changelog for PowerShell Universal.
---

# Changelog

## 

## 2.0.2 - 6/7/2021

### Includes

* UniversalDashboard - v3.4.2
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Changed

#### Dashboard

* Fixed an issue where the integrated environment wouldn't log
* UDv3 - Fixed an issue where Show-UDIcon would not work without an icon

#### Platform

* Fixed an issue where the favicon was missing on the admin console
* Rolling back a change to session time out for the admin console as it was causing problems with forms resetting 

## 2.0.1 - 6/4/2021

### Includes

* UniversalDashboard - v3.4.1
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Added

#### Platform

* Added $Headers, $Cookies, $RemoteIpAddress, $LocalIpAddress, $RemotePort, and $LocalPort to authentication.ps1

### Changed

#### Automation

* Fixed an issue where Get-PSUScript would throw an exception when the script didn't exist

#### Dashboard

* UDv3 - Fixed an issue where New-UDTableTextOption was not exported in the module manifest.
* UDv3 - Fixed an issue where Show-UDTooltip -Icon didn't work. 
* UDv3 - Fixed an issue where New-UDAlert was not exported in the module manifest.
* UDv3 - Fixed an issue where the New-UDCodeEditor didn't have a default parameter set provided

#### Platform

* Fixed an issue where many app tokens could be created automatically 
* Hide Trial Info button if platform is licensed
* Enabled BinaryFormatter to allow for PowerShell remoting in an the integrated environment
* Fixed an issue where the LTS Docker container would not start
* Fixed an issue where Policy Defined identities would have a blank role in the Identities table 
* Fixed an issue where the session timeout modal would not be shown in the admin console

## 2.0.0 - 6/2/2021

{% hint style="warning" %}
Please see notes about [upgrading](get-started/getting-started/upgrading.md) from 1.x to 2.x
{% endhint %}

### Includes

* UniversalDashboard - v3.4.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.0
* UniversalDashboard.Style - 1.0.0

### Changed

#### API

* Fixed an issue api with space in the url
* Fixed an issue where a large API request could lock the browser UI

#### Automation

* Fixed an issue where a script would not be deleted from disk when deleted in PSU

### Added

#### API

* Integrated environment support
* Added support for $Cache: scope

#### Automation

* Tag Support
* Access Controls for Scripts
* Integrated environment support
* Added support for $Cache: scope 

#### Dashboard

* Added support for syncing components via git
* Added description to dashboard components. 
* Added description to dashboards
* Integrated environment support

#### Platform

* Plugin support 
* New Admin Console
* Added Tags and script tags
* Improved Access Controls
* Added support for notifications
* Add New-PSULoginPageLink cmdlet to add login links
* Integrated environment
* Add Remove-Item support for $Cache: scope

## 1.0 Changelog

The 1.x changelog can be found [here](https://docs.powershelluniversal.com/v/v1/changelog).

