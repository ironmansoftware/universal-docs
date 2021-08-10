---
description: Changelog for PowerShell Universal.
---

# Changelog

## 2.2.1 - 8/11/2021

### Includes

* UniversalDashboard - v3.5.2
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Changed

#### Automation

* Fixed an issue where a default value of \[DateTime\]::Now would cause the run script modal to show an error
* Increased the width of the run script modal to accommodate longer parameter names
* Enforce authorization for the Hangfire dashboard
* Fixed an issue where naming scripts with certain characters would cause them to fail to save.

#### User Interfaces

* Pages: Fixed an issue where the page table would not show that authentication was enabled
* Pages: Fixed an issue where the page would flicker when a chart was on the page 
* Pages: Fixed an issue where a component wouldn't show up after adding it to the page 

#### Platform

* Fixed an issue where upgrading Windows PowerShell could cause PSU to fail to start, run jobs or start dashboards
* Added display of execution environment PowerShell version
* Fixed an issue where redirect to login page would take about 5 seconds
* Fixed an issue where login wouldn't work correctly when going to admin page for OIDC and WS-Fed. 
* Added telemetry for page views
* Fixed an issue where you couldn't delete the last item \(Endpoints, scripts, dashboards, etc\)
* Fixed an issue where the configurations page would show an empty file name

## 2.2.0 - 8/2/2021

### Includes

* UniversalDashboard - v3.5.2
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Added

#### User Interfaces

* Added pages feature with new page designer
* Dashboards: Fixed an issue where dashboards wouldn't use the configured default environment
* Dashboards: Fixed an issue where auto-deploy would refresh the browser before setting the new settings 

### Changed

#### Automation

* Fixed an issue where if a script PS1 file didn't exist but was configured in scripts.ps1, it would cause all configuration to fail
* Fixed an issue where jobs could restart \(retry\) even after running successfully

#### Platform

* Reorganized admin console menu 
* Fixed an issue where the admin console would display an error when trying to load pages when not logged in
* Fixed an issue where the user name text color in the menu when using single sign on

## 2.1.4 - 7/28/2021

### Includes

* UniversalDashboard - v3.5.2
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Changed

#### Dashboard

* Fixed an issue where New-UDTable -Data would fail to show a table with a single record. 

## 2.1.3 - 7/26/2021

### Includes

* UniversalDashboard - v3.5.1
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Changed

#### API

* Fixed an issue where returning a $null from an API would cause it to fail

#### Automation

* Fixed an issue where the dashboard log would not update in real-time
* Fixed a memory leak that would cause memory to grow over several days of running jobs
* Fixed an issue where continuous jobs would show an invalid Next Execution time

#### Dashboard

* Fixed an issue where the dashboard log didn't have scroll bars
* Fixed an issue where multiple roles would not work with New-UDPage
* Fixed an issue where dashboards would be slow to start
* Fixed an issue where New-UDTable -LoadData would show an error when first loading
* Fixed an issue where New-UDTimepicker -Label wouldn't work
* Fixed an issue where pressing enter in a textbox would not submit a form

### Platform

* Fixed an issue where app tokens would be created automatically 
* Fixed an issue where the swagger documentation was not generated correctly 
* Fixed an issue where empty configuration files could cause problems
* Fixed an issue where Start-PSUServer would only listen on localhost
* Fixed an issue where the update check service would hold a copy of the database open and cause a memory leak

## 2.1.2 - 7/7/2021

### Includes

* UniversalDashboard - v3.5.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Changed

#### APIs

* Fixed an issue where endpoint content could fail to save.
* Fixed an issue where editing the environment for the API would result in the API no longer functioning

#### Automation

* Fixed an issue where the job parameter table was not visible on the job page
* Fixed an issue where you were unable to select a credential for a PSCredential parameter
* Fixed an issue where Next Execution would show an invalid date for Continuous schedules

#### Dashboards

* Fixed an issue where dashboard content could fail to save.
* Improved performance of dashboard auto-deploy
* Added DisableErrorToast to disable error toast messages within the UI
* Fixed an issue where dashboards would restart when adding\editing a variable even when DisableAutoStart was set

#### Platform

* Updating .NET 5.0 runtime version to support Windows Update KB5003638 and to mitigate CVE-2021-26701
* Changed template description input to textarea for more space
* Fixed an issue where the Execute role couldn't login to the admin console
* Fixed an issue where git sync would create a master branch on the remote if the directory wasn't empty

## 2.1.1 - 7/1/2021

### Includes

* UniversalDashboard - v3.5.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Changed

#### Automation

* Fixed an issue where the script was not displayed in the jobs table

#### Platform

* Reverting a change made to status code pages \(Unauthorized page\) because it causes issues with SSO \(Windows\WS-Fed\OIDC\)

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

