---
description: Changelog for PowerShell Universal.
---

# Changelog

## Changelog

## 3.2.5 - 8/19/2022

#### Dashboard

* Fixed an issue with New-UDForm -Schema where an error would be shown if -UiSchema was not used

#### Platform

* Improved profiling of configuration scripts to help identify slow changes in the admin console

## 3.2.4 - 8/18/2022

#### Automation

* Fixed an issue where jobs would fail to run when using SQL persistence.&#x20;

## 3.2.3 - 8/16/2022

#### Dashboards

* Fixed an issue where certain components would shrink in size when switching between dark and light theme when using persistent navigation.
* Fixed an issue where New-UDDashboard would not honor the NavigationLayout parameter in certain configurations

## 3.2.2 - 8/15/2022

#### APIs

* Fixed an issue where updating API environments would not work in admin console.

#### Automation

* Fixed an issue where pipeline output for simple types would not display correctly in the admin console pipeline output tab
* Fixed an issue where job parameter values would not be displayed in the admin console
* Fixed an issue where Switch and bool parameters would not change from false in the admin console
* Fixed an issue where $UAJob.Identity was $null

#### Dashboards

* Fixed an issue where content would be hidden when switching between light\dark theme when using a persistent navigation menu
* Fixed an issue where variables defined out of -LoadRows in New-UDDataGrid were not available in the script block

## 3.2.1 - 8/11/2022

#### Automation

* Fixed the performance of the jobs table in the admin console
* Set the jobs table to auto refresh when refocusing on it

#### Dashboard

* Fixed an issue where page loading skeletons would not be displayed properly
* Fixed an issue where the icon would not be displayed for New-UDAutocomplete with -Multiple and -LoadOptions set.
* Fixed an issue where New-UDDashboard -HideUserName would not work when specifying pages
* Fixed an issue where the menu would be available as a blank drawer when a page was loading that had LoadNavigation
* Fixed an issue where a temporary navigation menu would not close after navigating
* Fixed an issue where -BackgroundColor did not support rgb colors on New-UDChartJS

#### Platform

* The MSI installer will now list the log file path if it fails



## 3.2.0 - 8/9/2022

#### Breaking Change

* SQL Server encryption is enabled by default.

{% hint style="warning" %}
When upgrading to PowerShell Universal v3.2, you may need to update your connection string to accommodate this breaking change.&#x20;
{% endhint %}

#### Steps to Successfully Update SQL Connection String

These steps are required if your SSL server has a certificate not trusted by the PowerShell Universal server.&#x20;

1. Stop PowerShell Universal service.&#x20;
2. Open `%ProgramData%\PowerShellUniversal\appsettings.json`
3. Add `;TrustServerCertificate=True;` to your connection string.&#x20;
4. Perform Upgrade&#x20;

#### Automation

* Grey out disabled schedules
* Fixed an issue where setting a default value on a bool parameter would cause an issue with the admin console run script UI
* Fixed an issue with the scrollbars on the scripts page
* Added working directory support for scripts (integrated environment not supported)
* Added support for Endpoint Error and Endpoint Authentication Failed triggers
* View nested jobs as a tree view in the jobs table
* Hide nested and triggered jobs in the job table
* View nested jobs from a parent job
* Improved the display of internal errors when running jobs
* Fixed an issue where jobs that threw an internal error would have an incorrect start time.
* Fixed an issue where string\[] parameters with a ValidateSet attribute wouldn't be displayed correctly when creating a schedule
* Fixed an issue where creating a continous schedule with a delay of 0 would cause the schedule to fail during creation
* Add indicies to the Job table to speed up job retrieval for SQL persistence.
* Fixed issue where certain simple schedules had invalid CRON expressions

#### Dashboard

* Fixed an issue with UDTab -Icon spacing.
* Fixed an issue where the whole page would flicker when using Sync-UDElement
* Added Protect-UDSection
* Added OnCancel and CancelButtonText to New-UDStepper
* Added -UiSchema to New-UDForm
* Removed New-UDTabContainer from the UniversalDashboard module manifest.
* Fixed an issue where -Icon would cause an overlap in New-UDTextbox
* Fixed an issue where an Object Reference exception would be thrown when using Invoke-Command
* Added New-UDDataGrid
* Fixed an issue where New-UDUpload wouldn't work when using SQL peristence.
* Updated to the lastest version of the MUI Date and Time pickers
* Fixed an issue where -Format on New-UDDatePicker would not have any effect
* Added dark theme support for the Ant Design theme.
* Fixed an issue where some of the cmdlet help was missing
* Fixed an issue where click navigation links would cause the navigation to collapse.
* Fixed an issue with New-UDTextbox where when a -Mask was specified an a string wasn't specified for -Value an error would be shown
* Fixed an issue with New-UDSelect where when -Multiple was specified and the -DefaultValue was not an array, an error woul be shown
* Added a beta version of the new advanced dashboard editor

#### Platform

* Added the ability to reset git settings.
* Added support for OSX 12 ARM64
* Added DataMigration tool for moving data from LiteDB to SQL
* Fixed an issue where translations containing a single quote would break a translation file
* Improved the contrast of the highlighted text in the admin console dark theme editors
* Added support for Active Directory Default SQL authentication
* Fixed an issue where git sync would stop reporting history when the git history was in an invalid state
* Added process and runspace information.
* Fixed an issue where the groom job would throw an exception when trimming jobs when using SQL persistence.
* Implemented -Integrated for Sync-PSUConfiguration
* Tables in the admin console will now persist the selected page size.
* Enabled retry behavior for SQL persistence.
* Grant-PSUAppToken now supports granting multiple roles.
* Added HTTP endpoints to set cache data
* The input box for updating secret strings is now masked
* Added support for finding and installing prerelease modules
* Fixed an issue with git sync when using SQL persistence and multiple nodes.
* Fixed an issue where the groom job could fail and then would retry over and over again
* Fixed the documentation link for the PowerShell Protect page
* Fixed an issue where the git page would list the remote in place of the branch

## 3.1.6 - 7/27/2022

{% hint style="warning" %}
Known issue: You may experience an issue when upgrading to this version due to encryption handling for SQL connections. As a work around, you may need to include `Trusted Connection = True` in your connection string. You can read more about this issue [here](https://forums.ironmansoftware.com/t/powershell-universal-3-1-6/7487/3?u=adam).
{% endhint %}



#### Dashboard

* Fixed an issue where non-terminating errors could cause exceptions to be shown in dashboards.

#### Platform

* Fixed an issue where SQL persistence was using an outdated version of the MS SQL client.

## 3.1.5 - 7/25/2022

#### Platform

* Fixed an issue where git sync would throw errors and prevent history from being saved.&#x20;

## 3.1.4 - 7/19/2022

#### Automation

* Fixed an issue where Invoke-PSUScript could throw an object reference exception when using -Wait and -Integrated and no data was returned
* Fixed an issue where Invoke-PSUScript would not return Information output

#### Dashboards

* Fixed an issue where New-UDAutocomplete would not display icon

#### Platform

* Fixed an issue where naming a variable Database would cause issues with PSU configuration
* Fixed an issue where the Modules folder was returned in the script view.
* Fixed an issue where the translation provider would conflict with local T drives (TL drive now available)
* Fixed an issue where translation strings with single quotes would cause issues with the saved translation files

## 3.1.3 - 7/15/2022

#### Automation

* Fixed an exception that could be thrown while cleaning up schedules jobs that could result in job failures
* Fixed an issue where terminals would not start when using SQL persistence
* Fixed an issue where jobs could be retried even after the script was deleted when using SQL persistence.

#### Dashboards

* Fixed an issue where New-UDAutoComplete wouldn't display the selected items

#### Pages

* Fixed an issue where certain buttons weren't visible in the dark theme
* Fixed an issue where failures to load the page's data source would cause the page to fail to load completely

#### Platform

* Fixed an issue with persisting the git sync interval setting
* Fixed an issue with ARM64

## 3.1.2 - 7/14/2022

#### Automation

* Disabled Hangfire automatic retry of jobs because it would cause problems with SQL persistence
* Fixed an issue where terminal commands would not complete successfully when using SQL persistence
* Fixed an issue where Invoke-PSUScript -Integrated wouldn't work when using SQL persistence

#### Platform

* Fixed an issue where the Name of the language was not displayed in the translations page
* Fixed an issue where problems with the roles.ps1 file would prevent access to PSU. The platform will now fallback to the default roles if there are issues.
* Fixed an issue where notifications would not be displayed when using SQL persistence

## 3.1.1 - 7/13/2022

#### Dashboard

* Fixed an issue where New-UDTextbox -Mask's label wasn't aligned correctly.
* Fixed styling of the No Data cell in server-side UDTables

#### Platform

* Fixed issues editing translations in the admin console

## 3.1.0 - 7/11/2022

#### APIs

* Fixed an issue where creating an endpoint via the Management API would not return said API endpoint
* Fixed an issue where Get-PSUEndpoint -Url did not return APIs.

#### Automation

* Added a more clear link to job details from the Jobs page
* Added option to display timestamps in absolute time
* Added a more clear link back to a script from the jobs page
* Added a more clear link from a job to a script
* Added Job Handshake Timeout to the settings page
* Added support for storing terminal command history
* Invoke-PSUScript will now write errors and warnings generated by jobs when using -Wait
* Fixed an issue where the System Default time zone would set the schedule as UTC
* Fixed an issue where the credential would not be honored by a schedule if set on a script
* Added a button to view raw log output
* Fixed an issue where you needed to specify a body when invoking a script from an Management API

#### User Interfaces

* Dashboards: Fixed an issue where the UDSelect label would be indented
* Dashboards: Added -Variant to New-UDSelect
* Dashboards: Fixed an issue where UDSelect would always have the first item selected even if -DefaultValue or -Value was not set.
* Dashboards: Added -Size to New-UDIconButton
* Dashboards: Added -Raised to New-UDCard
* Dashboards: Added -Size to New-UDSwitch
* Dashboards: UDFloatingActionButton now defaults to BottomRight
* Dashboards: Added -Style, -HeaderStyle, -FooterStyle, -ContentStyle and -Dividers to Show-UDModal
* Dashboards: Fixed an issue where dashboard memory was not reported.
* Dashboards: Fixed an issue with the display of a server-side table with no data
* Dashboards: Added copy\paster support to dashboard terminals
* Dashboards: Added -DefaultValue to New-UDRadioGroup
* Dashboards: Added -ShowLoading, -LoadingIndicator, and -LoadingPosition to New-UDButton
* Dashboards: Fixed an issue where Set-UDElement wouldn't properly update the selected value in New-UDSelect
* Dashboards: Fixed an issue where New-UDTable autocomplete filters would compress
* Dashboards: Fixed an issue where Out-String would not work without -Width in Windows PowerShell
* Dashboards: Fixed an issue where New-UDTreeView wouldn't expand when using dynamic trees
* Dashboards: Added Dutch language support (nl) to New-UDDatePicker and New-UDTimPicker
* Dashboards: Fixed an issue where Sync-UDElement would cause problems with Show-UDModal
* Dashboards: Added -SessionTimeout to New-UDDashboard
* Dashboards: Added -Unmask to New-UDTextbox
* Dashboards: Fixed an issue where masked UDTextbox would throw a JS error
* Dashboards: Fixed an issue where -Defaultvalue wouldn't be set right away with New-UDSelect
* Dashboards: Added -FullWidth to New-UDStack
* Dashboards: Fixed an issue where New-UDUpload would show two buttons
* Dashboards: Added -MinimumDate and -MaximumDate to New-UDDatePicker
* Dashobards: Fixed an issue where the Unauthorized page would not be shown when a user didn't have access to a page (404 page shown)
* Pages: Added support for HTML and markdown in cards
* Pages: Show page size changer for Tables

#### Desktop

* Suppress an exception thrown when a hotkey was already registered

#### Platform

* Moved the Save Changes button on the General settings page to be more accessible
* PowerShell versions are now updated dynamically when environments are loaded
* Fixed some issues with the admin console on smaller resolutions
* Fixed an issue where PSModulePath would be out of order for Windows PowerShell causing some modules to fail to load.
* Fixed an issue where Get-PSUComputer would not return a value
* Updated the PowerShell SDK to 7.2.5 for the integrated environemnt
* Added support for disabling a role
* Removed support for "high performance runspace pools" because they offer the same performance as the standard ones
* Variables from variables.ps1 are now defined in other PS1 configuration files
* Added ProjectUri to Templates
* Added proxy support for licensing and marketplace.
* Added -CssStylesheetIntegrity to New-PSULoginPage
* Added Remove-PSUDashboard
* Added Get-PSUDashboard -Name parameter
* Added an option to hide the Run As setting throughout the admin console.
* Added -RemoveSecret to Remove-PSUVariable to delete secrets from vaults
* Added Import-PSUSecret to load secret info from vaults
* Added translation support for APIs and Dashbaords
* Added support for configuring git sync in the UI
* Added an option to configure the git sync interval
* Fixed an issue where git sync changes would expand the entire table
* Sync-PSUComponent will now attempt to sync across all connected PSU instances
* Fixed an issue where the PowerShell Universal module would not work in Windows PowerShell
* Added a setting to enable splatting for all configuration files
* Fixed an issue where the DisableUpdateCheck setting did not work.
* Added the node name to the home page
* Fixed a display issue with the Persistent Runspace setting the admin console.
* Fixed a display issue when editing variables
* Fixed an issue where existing settings would not be shown when editing SAML2 authentication
* Fixed an issue where Set-PSUAuthenticationMethod would return a 404 error
* Fixed an issue where the MSI installer had some overlapping controls on one of the configuration pages.
* Fixed issue with editor autocompletion
* Added a display of the last time the git sync ran; even if there were no changes
* Fixed an issue where git commits would not display the correct changes in the commit
* Added the ability to see a diff of git changes
* Fixed an issue where Install-PSUServer\Upgrade-PSUServer -LatestVersion wouldn't install the correct version.
* Added -RequireMfa to Set-PSUAuthenticationMethod

## 3.0.6 - 6/30/2022

#### Platform

* Fixed an issue where PSModulePath was in an incorrect order causing modules to fail to load in Windows PowerShell

## 3.0.5 - 6/26/2022

#### Platform

* Rollback change to admin console due to issues with IntelliSense

## 3.0.4 - 6/26/2022

#### APIs

* Fixed an issue where endpoints defined by path would not reload when the target file changed on disk
* Fixed an issue where the endpoint test card would show a JavaScript error in the admin console

#### Dashboards

* Fixed an issue where New-Guid would not be found
* Fixed an issue where the DateTime filter for New-UDTable would display a JavaScript error
* Fixed an issue where -Title would not do anything when using New-UDPage
* Fixed an issue where -ShowRefresh would not do anything when specified on New-UDTable
* Fixed an issue where Invoke-UDEndpoint wouldn't properly setup the endpoint execution environment

#### Pages

* Fixed an issue where the validation API could not be cleared from a Form

#### Automation

* Fixed an issue with folder view for APIs not showing endpoints that were not part of a folder
* Fixed an issue where scripts would default to SilentlyContinue

#### Platform

* Fixed an issue where the modules page could present a javaScript error
* Fixed an issue with path autocompletion

## 3.0.3 - 6/17/2022

#### Platform

* Fixed an issue where creating a string secret variable would not set the secret in the vault
* Fixed an issue where updating environments would create corrupt environments.ps1 files

## 3.0.2 - 6/16/2022

#### APIs

* Fixed display issue with Endpoint folder view

#### User Interfaces

* Dashboards: Fixed an issue where certain theme properties would not be set (for example, body1 typography)
* Dashboards: Fixed an issue where New-UDIconButton -OnClick would not receive all variables
* Dashboards: Fixed an issue where the session timeout modal had an error where the refresh button should be.
* Dashboards: Fixed an issue where Invoke-UDEndpoint couldn't use $Session variables
* Dashboards: Fixed an issue where component padding and margin was incorrect for UDPaper, UDCard, UDAppBar, UDBButton, UDChip, and UDIconButton
* Pages: Fixed an issue where a card would show an error if data was not loaded correctly

#### Automation

* Fixed an issue where Get-PSUJob would not honor -OrderBy or -OrderDirection
* Fixed an issue where navigating to a job from the failed jobs page would result in a blank page

#### Platform

* Fixed an issue where Okta SAML2 would not work with PSU.
* Fixed an issue where the Universal module was not imported automatically and secrets would fail to load
* Fixed an issue where the Universal module could be loaded from elsewhere on the system causing an assembly load error due to the wrong version being loaded.
* Fixed an issue where Git status would be returned in ascending order
* Fixed an issue where the MSI installer would prompt for configuration options during an upgrade.
* Fixed an issue where online license keys would fail to activate when using SQL persistence

## 3.0.1 - 6/14/2022

* Dashboards: Fixed an issue where New-UDTable would default to a max-height of 0
* Fixed an issue where the v3 UniversalDashboard module was listed as pre-release&#x20;

## 3.0.0 - 6/14/2022



### Removed

#### User Interfaces

* Dashboard: Removed UDv2 Framework
* Dashboard: Merged all components into the v3 framework.
* Removed UA aliases on PSU cmdlets
* Secret variables are no longer automatically included in environments

### Added

#### APIs

* Added support for multiple API environments
* Added support for multiple methods for an endpoint
* Added folder view for APIs
* Added Live Log view

#### Automation

* Added support for multiple job agents via SQL support

#### Desktop

* Added support for triggering scripts on system events
* Hot key scripts will now receive a $HotKey parameter
* Added support for triggering scripts based on file associations
* Added support for triggering scripts based on custom protocols
* Added Show-PSUPage to display pages from the desktop client.

#### User Interfaces

* Dashboards: Added New-UDStack
* Dashboards: Added -Schema to New-UDForm
* Dashboards: Added New-UDTimeline and New-UDTimelineItem
* Dashboards: Added New-UDBadge
* Dashboards: Added -Sx and -Component to New-UDStyle
* Dashboards: Added dashboard templates to the create dashboard dialog.
* Dashboards: Added -Beat, -Fade, -BeatFade, and -Shake to New-UDIcon
* Dashboards: Added support for -OnRowExpand in New-UDTable
* Dashboards: Added support for Sync-UDElement against new New-UDTable
* Pages: Added a card component

#### Platform

* Added $Secret: scope for accessing secrets
* Added repository editor to edit all files in the repository.
* Added Settings \ General \ Diagnostics live log view
* Added Live Log view to Authentication and Authorization scripts.
* Added SQL server support for persistence
* Support for notification levels (Information, Warning, Error)
* Added support for any type in variable values
* Display build ID in the admin console
* Added PowerShell Protect integration
* Added support for hosting PowerShell Universal in a nested URL
* Added method selectors to the API endpoint page
* Added Copy published folder button
* Add Get-UDTheme and a default Ant Design theme

### Changed

#### APIs

* Serialization depth is now set to 5
* ErrorAction now defaults to Stop

#### Desktop

* Fixed an issue where you couldn't create hotkeys within the admin console.
* Fixed an issue where executing a hot key wouldn't work
* Fixed an issue where PowerShellUniversal.Desktop.exe was not included in the installer

#### User Interfaces

* Dashboards: No longer deploy built in assets by default
* Dashboards: Reduced bundle size
* Dashboards: Updated to MUIv5
* Dashboards: Dashboard logs are now live
* Dashboards: Fixed an issue where New-UDTransition would throw an error

#### Platform

* Updated to .NET 6.0
* Settings and Login page scripts now use splatting when saving
* Fixed an issue where copy and paste would not work in terminals
* Fixed an issue where live logs would be blank
* Cleaned up the MSI installer to have better UX
* Identities now support assigning multiple roles
* PSU now locates all registered module repositories on the modules page
* Endpoints now check syntax before saving to endpoints.ps1
* Fixed an issue where calling New-PSUSchedule from a dashboard wouldn't set the NextExecution time for a OneTime schedule
* Fixed an issue where New-PSUScript wouldn't work within a dashboard
* Fixed an issue where Get-PSUCache wouldn't return cached items
* Fixed an issue where Get-PSUCache wouldn't unwind arrays
* Connect-PSUServer now returns information about the session after connection
* Merge all fixes from 2.x

###
