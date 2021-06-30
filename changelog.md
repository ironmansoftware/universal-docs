---
description: Changelog for PowerShell Universal.
---

# Changelog

## 2.1.0 - 6/29/2021

### Includes

* UniversalDashboard - v3.5.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Added

#### Automation

* Added Name to schedules
* Added Description to variables

#### Dashboard

* Added Run As support for dashboards
* Added an error toast when an error happens in an endpoint
* UDv3 - Added -ButtonVariant to New-UDForm
* Added $ClaimsPrincipal variable to dashboard endpoints
* UDv3 - Added a ValidateSet to the -Color parameter of New-UDButton
* UDv3 - Added Persistent to Show-UDToast
* UDv3 - Added New-UDLayout
* UDv3 - Added -Icon to New-UDTable
* Added $DashboardName, $DashboardFilePath, and $DashboardBaseUrl to endpoints

#### Platform

* Added support for templates

### Changed

#### API

* Fixed an issue where descriptions would not persist when set in the admin console
* Fixed an issue where roles would not be populated when editing an endpoint

#### Automation

* Fixed an issue where you could not create a schedule with an environment in the admin console
* Fixed an issue where you could not create a schedule with a credential in the admin console
* Increased the Set-PSUCache limit to 32GB
* Fixed an issue with displaying nested scripts within the admin console

#### Dashboard

* By default, dashboards are now created in their own folder in the repository folder
* UDv3 - Fixed an issue where New-UDTable would fail to export a rendered column
* UDv3 - Hide logout button when using Windows authentication
* UDv3 - Fixed an issue where -SortType datetime would not function correctly on New-UDTable 
* UDv3 - Upgraded to the latest version of SignalR to fix issues with Chrome tab idling.
* UDv3 - Removed a restriction on what element was supported with New-UDListItem and -Icon
* Fixed an issue where the Operator role could not save dashboards
* Fixed an issue where users with no matching roles for a dashboard page would receive an error

#### Platform

* Fixed an issue where scroll bars were missing from editors and logs in the admin console
* Fixed an issue where you couldn't delete app tokens or schedules on the identity page
* Fixed an issue where the document title for the login page wouldn't update for custom login pages
* Fixed an issue where you couldn't clear run as credentials from scripts, schedules or dashboards
* Display integrated PowerShell version on environments page
* Fixed an issue where you couldn't create secrets with New-PSUVariable
* Fixed an issue where Windows authentication would not work
* Fixed an issue where standard \(online\) licenses would become inactive after some time
* Fixed an issue where setting the Security Environment to integrated would cause the service to fail to start.
* Fixed an issue where you couldn't clear roles once they were set.
* Fixed an issue where saving a role policy would not work

## 2.0.3 - 6/10/2021

### Includes

* UniversalDashboard - v3.4.3
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Added

#### Dashboard

* Added a Remove button to the components drawer

### Changed

#### API

* Fixed an issue where the $UserName would not be available in APIs

#### Automation

* Fixed an issue where string\[\] types could not be used with ValidateSet attributes
* Fixed an issue where you could select an environment in the run dialog even though it was set on the script
* Fixed an issue where you could select a credential in the run dialog even though it was set on the script
* Fixed an issue where the credential selector was missing in the script properties dialog

#### Dashboard

* Fixed a null reference exception that could happen when stopping a dashboard
* Fixed an issue where the access denied page was missing
* UDv3 - Fixed an issue where after logging out and logging back in the user wouldn't go back to the dashboard

#### Platform

* Added loading button to modals in the admin console
* Fixed an issue where the close icon wouldn't load correctly for modals in the admin console
* Fixed an issue where large tables could overflow off the screen in the admin console
* Fixed an issue where the total memory usage would be reported as NaN when no dashboards were running
* Fixed an issue where leaving the admin console tab and coming back would clear modal forms
* Fixed an issue where the session time out dialog would not be shown in the admin console
* Fixed an issue where a JavaScript error could be shown when loading a dashboard page
* Fixed notification text for dashboard restarts
* Fixed an issue where Windows PowerShell 5 would fail to start dashboards and APIs.
* Fixed MSI upgrade from 1.5 to 2.0

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

