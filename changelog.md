---
description: Changelog for PowerShell Universal.
---

# Changelog

## 2.8.1 - 2/10/2022

### Includes

* UniversalDashboard - v3.10.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.3
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

***

### Changed

#### User Interfaces

* Dashboards: Fixed an issue where dashboard components would not be loaded
* Dashboards: Improved endpoint execution performance
* Dashboards: Improved endpoint memory usage
* Dashboards: Increased timeout for Get-UDElement
* Pages: Fixed an issue with user name location
* Pages: Fixed an issue where scripts that returned a warning would cause a form to reset

#### Platform

* Fixed an issue where the parse error request would happen too frequently
* Fixed an issue where the claims cache would not be reset if roles changed

## 2.8.0 - 2/7/2022

## Includes

* UniversalDashboard - v3.10.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.3
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

***

## Removed

### User Interfaces

* Dashboards: Removed the Start-UDDashboard cmdlet from the UniversalDashboard module manifest

## Added

### API

* Added support for large file downloads from endpoints.
* Added -Timeout to New-PSUEndpoint

### Automation

* Added support for Enter-PSSession and Exit-PSSession
* Added -Integrated support to Get-PSUJob
* Added support for parameter sets when executing scripts
* Desktop Mode: Added support for executing scripts with global hotkeys
* Added -DiscardPipeline to New-PSUScript

### User Interfaces

* Pages: Added default page size setting to table
* Dashboards: Added -Label, -CheckedLabel, and -UncheckedLabel to New-UDSwitch
* Dashboards: Added -HeaderContent to New-UDPage
* Dashbaords: Added basic toggle to dashboard page
* Dashboards: Added -PaginationLocation to New-UDTable

### Platform

* Added IntelliSense to editors.
* Added Format (F8) support to editors.
* Added Debugging Tools
* Added Runspace Recycling option to reduce memory usage
* Added a confirmation before enabling or disabling authentication methods
* Added a link to create run as credentials when none are defined
* NuGet Package Management provider will be installed if it does not exist

## Changed

### Automation

* Fixed an issue where PowerShell 7.2 would include ANSI escape characters in job logs.
* Fixed an issue where renaming a script would not work
* Fixed an issue where the documentation link for Terminals was incorrect
* Fixed the ambiguity in the "cancel job" confirmation prompt

### User Interfaces

* Fixed an issue where the dashboard control buttons would be missing when One-Way git sync was enabled.
* Pages: Fixed an issue where the form text output would not expand to the container height
* Pages: Fixed an issue where unauthenticated pages would reset while loading causing forms to restart.
* Pages: Improved the editor tools layout.
* Dashboards: Fixed an issue where the theme setting would not persist.
* Dashboards: Updated the example dashboard
* Dashboards: Fixed an issue where a column named "version" would not work in UDTable.
* Dashboards: Fixed an issue where New-UDDatePicker could not be cleared
* Dashboards: Fixed an issue where typing the entire text of an item in New-UDAutocomplete would not perform a OnChange. You will still need to press enter to select the item.
* Dashboards: Improved memory usage
* Dashboards: Fixed an issue where sessions and endpoints would not be reported for the integrated environment
* Dashboards: Only the updated dashboard will auto-deploy when saved
* Dashboards: Fixed an issue where New-UDTable would not fill the width of its container
* Dashboards: Fixed an issue where param blocks would cause an error in dashboards
* Dashboards: Fixed an issue where -Multiple on New-UDAutoComplete could cause a JavaScript error
* Dashboards: Fixed an issue where -Multiple on New-UDAutoComplete with -OnLoadOptions wouldn't clear the typed text after selection
* Dashboards: Fixed an issue where dynamic pages would appear in navigation
* Dashboards: Built in components (Charts, Style, Map, CodeEditor, Editor) are now automatically added to dashboards

### Platform

* Improved handling of invalid OIDC configurations.
* Fixed an issue where the Copy button would be missing from the app token page when One-Way git sync was enabled.
* Fixed an issue where Set-PSUSetting -ScriptBaseFolder would not take effect when using the REST API
* Fixed an issue where Get-PSUFolder -Name would return a 404
* The user name field now receives auto focus on the login page
* Service will continue to attempt activation once per hour if it fails when the license is installed
* Fixed an issue where LiteDB would not work properly in an Azure App Service.
* Reduced the memory usage of the PowerShell Universal server and integrated environment
* Fixed an issue where more than the designated amount of runspaces could be allocated
* Updated the version of Microsoft.Identity.Client that is referenced
* Fixed an issue where Application Insights data would not be reported

## 2.7.4 - 2/4/2022

### Includes

* UniversalDashboard - v3.9.2
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.3
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

### Changed

#### Platform

* Fixed an authorization bypass issue

## 2.7.3 - 1/21/2022

## Includes

* UniversalDashboard - v3.9.2
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.3
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

## Changed

### Platform

* Fixed an issue where the SAML2 integration would get stuck in a redirect loop
* Fixed an issue with the UI for SAML2

## 2.7.2 - 1/16/2022

## Includes

* UniversalDashboard - v3.9.2
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.3
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

## Changed

### User Interaces

* Dashboards - Fixed an issue were Show-UDToast would show an error with the default parameters.

## 2.7.1 - 1/14/2022

## Includes

* UniversalDashboard - v3.9.1
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.3
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

***

## Changed

### Automation

* Fixed an issue where creating a schedule with a string array parameter would not work properly
* Fixed an issue where New-PSUSchedule -Integrated would not work with parameters
* Fixed an issue where you couldn't view jobs or scripts when using Windows Auth and FQDN server names
* Fixed an issue where terminals wouldn't work when using Windows Auth and FQDN server names

### User Interfaces

* Pages: Fixed an issue where table columns "sortable" property would not be persisted.
* Pages: Fixed an issue where pages would not be listed after creating a new page
* Pages: Fixed an issue where you couldn't execute anonymous scripts from unauthenticated pages
* Pages: Fixed an issue where you couldn't view pages when using Windows Auth and FQDN server names
* Dashboards: Fixed an issue where the dashboard console would not work in Windows PowerShell
* Dashboards: Fixed an issue where a $type property was added to $EventData in endpoints
* Dashboards: Fixed an issue where New-UDAutocomplete would not display the selected value
* Dashboards: Fixed an issue where New-UDTable margin did not match other elements.
* Dashboards: Fixed an issue where Show\Hide-UDToast would allow an invalid ID
* Dashboards: Fixed an issue where you could not clear the date filter on New-UDTable

### Platform

* Fixed an issue where setting claim type and claim value would not work from the UI
* Fixed an issue where pressing Ctrl+S would not save within the editors

## 2.7.0 - 1/11/2022

## Includes

* UniversalDashboard - v3.9.1
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.3
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

***

## Added

### Automation

* Added support for randomly delaying a schedule from 0 to 60 seconds to prevent all schedules of the same time frame from running all at once

### Platform

* Added an option to create app tokens that do not expire
* Added -Integrated support to the \*-PSUSchedule cmdlets

## Changed

### APIs

* Fixed an issue where endpoints could be created without a leading /

### Automation

* Fixed an issue where terminals would not display non-terminating errors

### User Interfaces

* Dashboard: Fixed an issue where New-UDSelectGroup would not work in New-UDForm
* Dashboard: Fixed an issue where entering text in a masked UDTextbox would cause loss of focus
* Dashboard: Fixed an issue where New-UDChartJSMonitor would not use color arrays for background or borders
* Dashboard: Improved logging for dashboard errors
* Pages: Fixed an issue where custom roles could not view pages
* Pages: Fixed an issue where identities authorized with app tokens could not view pages
* Pages are now displayed to non-default roles in the admin console

### Platform

* Updated to new version of Secret Management module
* Fixed an issue where PowerShell Universal wouldn't start properly on Linux.
* Fixed an issue where setting the default paths for automation wouldn't work in the admin console
* Fixed an issue where the Credential Manager vault would attempt to be registered on non-Windows systems
* Fixed an issue where the default secret store password was not set in appsettings.json on non-Windows systems
* Fixed an issue where errors would not be logged from the secret management module in jobs
* Fixed an issue where claim to role mapping would not work
* Fixed an issue where installing a module would not work if the Modules folder did not exist

## 2.6.2 - 12/17/2021

## Includes

* UniversalDashboard - v3.9.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

***

## Known Issues

Some users are still experiencing a service crash related to the secret store. If you experience a crash while starting the service, we recommend installing version 2.5.5. We are continuing to investigate.

## Changed

### User Interfaces

* Dashboard - Fixed an issue where nested elements may not display

### Platform

* Fixed an issue where using a non-standard secret vault would not work from the UI
* Fixed an issue where a crash could occur when multiple jobs attempted to read from the secret store.

## 2.6.1 - 12/15/2021

## Includes

* UniversalDashboard - v3.9.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

***

## Changed

### Automation

* Fixed an issue where PSCredential parameters would not be passed correctly to scripts

### Platform

* Changed the default web.config setting back to OutOfProcess
* Fixed an issue where InProcess hosting in IIS would not work
* Fixed an issue where the service could hang during startup
* Fixed an issue where creating a secret could throw an error

## 2.6.0 - 12/14/2021

## Includes

* UniversalDashboard - v3.9.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

***

## Known Issues

* The default web.config is set to InProcess hosting model rather than the previously set OutOfProcess hosting model. You will need to update the web.config if you would like to us OutOfProcess.

## Removed

### User Interfaces

* Dashboards - Removed -\*Offset parameters from New-UDColumn because they did not do anything

## Added

### API

* Added $ClaimsPrincipal object to API requests
* Added support for setting parameters via JSON properties

### Automation

* Added warning state to jobs
* Added support for terminals

### User Interface

* Dashboard: Add support for -FilterType 'date' in New-UDTable
* Dashboard: Added -Subheader to New-UDCardHeader
* Dashboard: Added Invoke-UDForm
* Dashboard: Added -Leaf, -Icon and -ExpandedIcon to New-UDTreeItem
* Dashboard: Added -Color to all compatible components
* Dashboard: Added Start-UDDownload
* Pages: Added support for Date and Time columns in tables.
* Pages: Added support for searching in tables
* Pages: Added support for showing scroll bars for tables.
* Pages: Added support for an icon in table headers.
* Pages: Added Size property to the table.

### Platform

* Added --appsettings command line option to specify location of appsettings.json file
* Added support for git sync push only
* The Git status table now lists the files that were changes and the change type
* Added support to New-PSUVariable for creating PSCredentials.
* Added the ability to hide credentials from the Run As dialog
* Added a dialog for viewing the current user's claims
* Added support for setting -ClaimType and -ClaimValue on roles to assign claims directly to roles
* Added PackageManagement 1.4.7 and PowerShellGet 2.2.5 to the standard install.
* Added support for storing secrets in the Microsoft SecretStore
* Added desktop mode

## Changed

### Automation

* Fixed an issue where scripts deleted in PSU with absolute paths would be deleted in their source location.
* Fixed an issue where jobs marked as Cancelling would not be groomed
* Fixed an issue where a parameter named -tag would prevent scripts from executing in the admin console
* Fixed an issue with creating folders on Linux and mac systems.
* Fixed an issue where running jobs under alternate credentials could result in an Access Denied error
* Fixed an issue where the -Credential parameter of New-PSUSchedule would not be persisted from the UI
* Fixed an issue where New-PSUSchedule -Condition would not work properly
* Fixed an issue where you should not call Get-PSUScript for scripts in a folder with -Integrated

### User Interfaces

* Dashboard - Fixed an issue where $EventData would be $null for Switches and Checkboxes
* Dashboard - Fixed an issue where display $false or 0 in UDTable would not work
* Dashboard - Fixed an issue where a user's theme preference would not be maintained
* Dashboard - Fixed an issue where Start-PSUDashboard was not exported from the Universal module.
* Dashboard - Enforce a ValidateRange parameter (0, 10) on -Spacing for New-UDGrid
* Dashboard - Fixed an issue where -Align on New-UDTypography would not work
* Dashboard - Fixed an issue where -TitleAlignment would not work on New-UDCard
* Dashboard - Adjusted style of UDTable to promote headers and title.
* Dashboard - Fixed an issue where New-UDSwitch $EventData would be an array
* Dashboard - UDUpload now supports uploads over 2 GB
* Dashboard - Fixed an issue where UDAutocomplete -Multiple wouldn't behave correctly with OnLoadOptions.
* Dashboard - Fixed an issue where the logout button would be shown for in dashboards when it should not be.
* Dashboard - Fixed an issue where vertical tab content wouldn't take up 100% of it's container
* Dashboard - Fixed an issue where Show-UDToast would not work with FontAwesome v5 icons
* Pages - Tables will now scroll rather than exceed the bounds of their designer window
* Pages - Fixed an issue where scripts in folders would not work as a data source
* Pages - Fixed an issue where pages would not be listed in some environments with Windows authentication

### Platform

* Fixed an issue where an error in the authentication.ps1 file would cause the Universal server to stop functioning.
* Hide some properties of scripts and dashboards when first creating a script or dashboard
* Fixed an issue where the custom admin console title and logo would not work
* Fixed an issue where -AdminConsoleLogo and -AdminConsoleTitle could not be set over the REST API via Set-PSUSetting
* Settings.ps1 is now generated as a multi-line command to make it easier to read
* Updated to Microsoft.PowerShell.SecretManagement version 1.1.1.
* Fixed an issue where the PSModulePath would be appended repeatedly in the integrated environment
* Fixed an issue where restarting a web app in Azure would cause it to fail to start

## 2.5.5 - 11/24/2021

### Includes

* UniversalDashboard - v3.8.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

### Changes

#### API

* Fixed an issue where Windows auth outside of IIS and client certificate authentication would cause 500 errors in REST APIs.

## 2.5.4 - 11/15/2021

### Includes

* UniversalDashboard - v3.8.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

### 👍Changes

#### Automation

* Fixed an issue where Invoke-PSUScript -Integrated would not work with parameters
* Fixed an issue where using blocks in script block content could cause scripts to not load properly

#### Platform

* Fixed an issue where invalid authenticationMethod.ps1 file could break authentication
* Fixed an issue where enabling client certificate authentication would result in a 500 error

## 2.5.3 - 11/12/2021

### Includes

* UniversalDashboard - v3.8.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

### 👍Changed

#### Platform

* Fixed an issue where an invalid authentication.ps1 file would be generated when editing authentication in the admin console.

If you cannot login to your PowerShell Universal platform due to an invalid authentication.ps1, please refer to this [forum thread.](https://forums.ironmansoftware.com/t/2-4-0-to-2-5-2-upgrade-breaks-something/5975/8?u=adam)

## 2.5.2 - 11/11/2021

### Includes

* UniversalDashboard - v3.8.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

### 👍Changed

#### Platform

* Fixed an issue where InProcess IIS hosting would not work
* Fixed an issue where using AppTokens with OIDC would not work.

## 2.5.1 - 11/9/2021

### Includes

* UniversalDashboard - v3.8.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

### 👍Changed

#### Platform

* Fixed an issue where hosting in IIS would not work
* Fixed an issue where Start-PSUServer was not available
* Fixed an issue where the wrong parameter types were generated for authentication methods
* Fixed an issue where Swagger documentation was not available

## 2.5.0 - 11/8/2021

### Includes

* UniversalDashboard - v3.8.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.2.0
* UniversalDashboard.Editor - 1.0.0
* UniversalDashboard.Style - 1.0.0

***

### 🐛 Known Issues

* Windows Authentication with IIS does not work properly.

### 💔Breaking Changes

* Grant-PSUAppToken no longer can generate app tokens locally and send them to the server

### ✔️Added

#### Automation

* Added support for displaying comment based help in the UI

#### User Interfaces

* Dashboard - Added -HeaderPosition to New-UDPage and New-UDDashboard
* Dashboard - Added New-UDMenu and New-UDMenuItem
* Dashboard - Added -FullWidth to New-UDSelect
* Dashboard - Added -HeaderColor and -HeaderBackgroundColor to New-UDPage and New-UDDashboard
* Dashboard - Added support for escape and clear-host in the dashboard console
* Dashboard - Added New-UDEditor component
* Dashboard - Added -Navigation and -NavigationLayout to New-UDDashboard
* Dashboard - Added -DisableStartupLogging to New-PSUDashboard
* Pages - Added support for IFrame component
* Pages - Added support for grouping pages in the navigation menu
* Pages - Added support for hiding the title and description on a page
* Pages - Added Password field to forms
* Pages - Added support for setting a page URL to /

#### Platform

* Added page size drop down to tables in the admin console
* Added server side configuration of authentication
* Added startup scripts to environments
* Added $PSUEnvironment variable to all endpoints
* Added support for creating and editing modules
* Added support for installing modules from the PowerShell Gallery
* Added support for setting secrets when One-Way git sync is enabled
* Added support for identifying when a secret variable does not exist in the vault.
* Added the tzdata package to the dockerfile to correctly support time zones on Linux
* Added support for SAML2 authentication
* Added support for custom authentication configuration via PowerShell script blocks.
* Added support for customizing the admin console title and logo
* Added a link to the hangfire details page from the Settings \ General \ Diagnostics page
* Added support for integrated cmdlet transport

### 👍Changed

#### API

* Fixed an issue where returning multiple API responses from an API endpoint would consume all CPU

#### Automation

* Updated to the most recent version of Hangfire
* Fixed an issue where setting the Time Out value for a schedule in the UI would not work
* Fixed an issue where editing schedules would not work correctly
* Fixed an issue where Pnp.PowerShell would not work in Windows PowerShell jobs
* Fixed an issue where New-PSUScript -ScriptBlock would not work against the REST API

#### User Interfaces

* Dashboard: Fixed an issue where New-UDTextbox -Multiline would not allow you to enter additional lines
* Dashboard: Fixed an issue where New-UDTransferList would only show the first selected value in -OnChange $EventData
* Dashboard: Fixed an issue where New-UDTransferList would not should the name\value pair for the default selected items
* Dashboard: Fixed issue where the -Title parameter of New-UDDashboard would not set the title
* Dashboard: Fixed an issue where the dashboard console would not accept backspace
* Dashboard: Fixed an issue where nested UDExpansionPanels would be arrange horizontally
* Dashboard: Fixed an issue where dashboards could be marked as stopped after server restart
* Dashboard: Fixed an issue where New-UDDrawer persistent would hide the content of the page with no way to close it
* Dashboard: Fixed an issue with New-UDUpload and integrated environments
* Dashboard: Fixed an issue where New-UDUpload would not work correctly in New-UDForm
* Pages: Fixed an issue where specifying a URL for a page that starts with a / would cause the page to fail to load
* Pages: Fixed an issue where specifying a URL for a page would prevent it from working in navigation
* Pages: Fixed an issue where going directly to a page with a custom URL would not work

#### Platform

* Fixed an issue where retrieving an app token by ID would not work if you were an administrator
* The folder\list view setting in the Scripts page is now persistent
* Removed the dependency on System.IdentityModel.Tokens.Jwt in the Universal module
* Fixed an issue where administrators couldn't clear notifications with one-way git sync enabled
* Fixed an issue where app tokens couldn't be generated when one-way git sync was enabled
* Fixed an issue where git status was not visit to administrators when one-way git sync was enabled
* Fixed an issue where administrator and operator roles would be changed to an execute role when one-way git sync was enabled.
* Fixed an issue where PSModulePath could grow too long and prevent the environment from being configured correctly
* Fixed an issue where you could not revoke app tokens or retrieve individual tokens
* Fixed an issue where git sync status would display an invalid time stamp
* Fixed an issue where tags would not work properly if a color wasn't set
* Added a backdrop to the session expired notification so you can't navigate the admin console when not authenticated
* Fixed an issue where Set-PSUCache -SlidingExpiration would not be honored.

## 2.4.1 - 10/21/2021

### Includes

* UniversalDashboard - v3.7.1
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

***

### Changed

#### User Interfaces

* Dashboard - Fixed render issue with New-UDIconButton
* Dashboard - Fixed an issue where New-UDUpload -OnChange did not behave the same as the previous version

#### Platform

* Fixed an issue where authorization policies would throw an exception and not log why it happened

## 2.4.0 - 10/12/2021

### Includes

* UniversalDashboard - v3.7.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Breaking Change

* Due to an issue with roles for pages, you will need to reset roles for existing pages after upgrade

### Added

#### APIs

* Added support for tagging endpoints
* Added the ability to filter endpoints by tags

#### Automation

* Added the ability to pause a schedule
* Added support for changing the base folder for storing scripts
* Added -Wait parameter to Invoke-PSUScript to wait for a script to return and write pipeline output
* Added the ability to filter scripts by tags
* Added support for folders within the scripts page
* Added job timeout support
* Added job retry support
* Added -Delay to triggers
* Added -Condition to schedules

#### User Interface

* Dashboards - Added support for tagging dashboards
* Dashboards - Added the ability to filter dashboards by tags
* Dashboards - All visual components now support -ClassName parameter for specifying a CSS class to apply
* Dashboards - Added support for large files and New-UDUpload
* Dashboards - Added progress when uploading files with New-UDUpload
* Pages - Added the ability to export from Table in a Page
* Pages - Added support for Select controls in forms within a Page
* Pages - Added support for button columns within tables in a Page
* Pages - Added select, rating, number, date, time, and switch as form controls
* Pages - Added support for help text for fields
* Pages - Added support for hiding the header
* Pages - Form results will now show the error message when a job fails
* Pages - Added refresh interval to tables
* Pages - Added manual refresh to tables
* Pages - Added support for variables
* Pages - Added support for URLs
* Pages - Added Pie chart

#### Platform

* Added Home page dashboard in admin console
* Added Repository\Modules to PSModulePath
* Added Hide Home Page setting
* Added Modules page to view modules in each environment
* Added Impersonation support to published folders
* Added setting for configuring Microsoft log level
* Added the ability to download logs from the console
* Added support for developer license
* Added Ubuntu 20.04 docker image
* Added Remove-PSUServer and Update-PSUServer
* Added a notification page to view all notifications
* Added support for developer licenses.

### Changed

#### API

* Fixed an issue where objects return by Select-Object wouldn't serialize correctly
* Fixed an issue where the editor in the admin console would not show all the code without scrolling correctly
* Fixed an issue where descriptions would not show up in Swagger documentation
* Fixed an issue where parameters would not have the correct type in Swagger documentations.
* Fixed an issue where Swagger documents wouldn't update unless the server restarted
* Fixed an issue where saving on edit ErrorAction does not work in the admin console
* \-Depth 100 and -Compress added to the automatic serialization in endpoints.

#### Automation

* Catch an exception that could be thrown when attempting to parse pipeline output
* Fixed an issue where parsing pipeline output could cause an exception
* Fixed an issue where string\[] parameters would have a blank value by default
* Fixed an issue where the Pnp.PowerShell module would not load correctly
* Fixed an issue where string\[] parameters with a ValidateSet would not work correctly
* Fixed an issue where missing scripts could cause all schedules to fail
* Fixed an issue where scheduling a script with a Switch parameter would not work

#### User Interface

* Fixed an issue where roles with spaces would not work with pages
* Dashboard components are now read from the repository on start up
* Dashboards - Fixed an issue where overrides for MUI themes would not work
* Dashboards - Fixed an issue where UDUpload would look different than UDButton
* Dashboards - Fixed an issue where -Icon would not work on New-UDExpansionPanel
* Dashboards - Fixed an issue where clicking previous in a stepper could go back to the wrong step
* Dashboards - Fixed an issue where New-UDSkeleton was not exposed from the module manifest
* Dashboards - Improved performance of file updates
* Dashboards - Fixed an issue with New-UDDatePicker where the server time zone would be used for the default value
* Dashboards - Fixed an issue where you couldn't disable auto start in the admin console
* Dashboards - Removed back and home buttons from the dashboard maintenance page
* Dashboards - Fixed an issue where UDTable wouldn't display a column data if all row didn't have the table value
* Pages - Improved the performance of tables by caching query data
* Pages - Fixed an issue where renaming a page would create a new page
* Moved links to frameworks, components and marketplace to the dashboards page

#### Platform

* Fixed an issue where cache options would not be honored for Set-PSUCache
* Reorganized the general settings page
* Fixed an issue where setting the log level in the UI wouldn't have any effect
* Fixed an issue where accessing the swagger URL could return a 403
* Fixed an issue where roles couldn't be set on published folders in the admin console
* Fixed an issue where environments could not set wild card variables
* Variables for environments now default to \*
* License dialog is now a file upload rather than a text box
* Install-PSUServer now installs the server as a service on Windows, systemd service on Linux and can install to IIS.
* Fixed an issue where conflicting entity URLs could be specified. An error message is now shown.
* Fixed an issue where administrators would not be able to access the console when One-Way git sync was enabled
* Fixed an issue where non-terminating errors could cause configuration scripts to fail
* Fixed an issue where displaying many notifications could cause the admin console to freeze
* Operator and Executor roles can now create app tokens for themselves
* Administrators can now view all app tokens
* Single-file hosting is now deprecated and will be removed in v3
* Fixed an issue where using a custom login page wouldn't redirect to the correct URL after login
* Fixed incorrectly named Ubuntu docker images

## 2.3.2 - 10/2/2021

### Includes

* UniversalDashboard - v3.6.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Changed

#### Platform

* Fixed an issue where non-integrated environments would not work on Linux

## 2.3.1 - 9/17/2021

### Includes

* UniversalDashboard - v3.6.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Changes

#### Automation

* Fixed an issue where jobs could fail due to certain types of pipeline output

#### Platform

* Fixed an issue where global cache cmdlets would not work in non-integrated environments

## 2.3.0 - 9/14/2021

### Includes

* UniversalDashboard - v3.6.0
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Added

#### APIs

* Added support for PATCH HTTP method
* Added $UrlDefinition, $RequestId, $ConnectionId and $SessionId as built in variables.
* Added support for OpenAPI documentation for endpoints
* Added ErrorAction to the endpoint properties modal

#### Automation

* Added support for DisplayName attributes on script parameters
* Added support for $AccessToken and $IdToken in scripts

#### User Interfaces

* UDv3 - Added New-UDTransferList and New-UDTransferListItem
* UDv3 - Added -Variant, -ScrollButtons and -Centered to New-UDTabs
* UDv3 - Added -Disabled to New-UDTab
* UDv3 - Added -Hidden to New-UDTableColumn for including data with tables for export purposes but not to show in the table itself.
* UDv3 - Added -Locale to New-UDDatePicker and New-UDTimePicker
* Pages - Added support for showing progress in Forms
* Pages - Added support for showing text output in forms
* Pages - Added support for showing table output in forms
* Pages - Added support for customize the submit button text and icon
* Pages - Added support for handling feedback in scripts
* UDv3 - Added support for -IdleTimeout on New-PSUDashboard

#### Platform

* Added notification about default authentication and authorization.
* Added support for -CssStylesheet on New-PSULoginPage
* Added support for customizing the login page within the Admin Console
* Added a notification for when the license file fails to activate
* Added support for client certificate authentication
* Added support for PowerShell 6.x
* Added Modules to the Environment settings modal
* Added Git synchronization page
* Added support for specifying scopes in OIDC connection
* Added support for accessing additional user information passed from OIDC providers in the $UserInfo variable.
* Added Sync-PSUComponent to reload components on dashboards from APIs and Scripts

### Changed

#### API

* Fixed an issue where variables would not show up when the API was using the integrated environment
* Fixed an issue where authenticated APIs could fail if they had a param block without $Identity and $User

#### Automation

* Fixed an issue where the job end time would by UTC rather than local in triggers
* Fixed an issue where deleting a tag that was assigned to a script would cause the scripts page to fail to load
* Fixed an issue where failed jobs would have an invalid start date
* Fixed an issue where Completed and Failed jobs that produced no output would still show waiting for job logs on the job's page
* Fixed an issue where Hashtable output by jobs couldn't be viewed in the Pipeline Output view
* Fixed an issue where the job view would not update automatically
* Fixed an issue where progress was not shown on the job view
* Fixed an issue where the server could crash when a job was cancelled
* Fixed an issue where error action would display the numeric value rather than the name of the error action
* Fixed an issue where string\[] params would fail to work correctly

#### User Interface

* Fixed an issue where a base URL of / on a dashboard prevents pages from working
* UDv3 - Fixed an issue where New-UDPage -Url was not honored in default navigation
* Added links to scripts and APIs from the page designer
* UDv3 - Fixed an issue where passing empty data to -Data of New-UDTable would throw an error.
* UDv3 - Fixed an issue where New-UDTable sorting could result in an error on the page about toUpperCase not being defined
* UDv3 - Fixed an issue where null values in rows of New-UDTable would cause filters to fail
* Fixed an issue where dashboard logs could show an error
* Fixed an issue where dashboard logs would not clear when using Auto Deploy
* Put new log messages on the top of the dashboard log (reversed log order)
* UDv3 - Fixed an issue where using server-side exporting of UDTable wouldn't honor -IncludeInExport on columns
* UDv3 - Fixed an issue where using server-side exporting of UDTable wouldn't use the -Title in exports
* UDv3 - Fixed an issue where using server-side exporting of UDTable would change the case of the title in exports
* Pages - Fixed an issue where Statistics would display script output as \[object Object]
* Pages - Fixed an issue where Form checkboxes in pages would not send data
* Pages Fixed an issue where required fields in forms would not be enforced
* Pages - Fixed an issue where you could drag components when modals were open
* Pages - Cleaned up the properties dialog and toolbox

#### Platform

* Swagger documentation now requires authentication to view
* MSI installer now verifies that .NET 4.7.2 or later is installed
* Fixed an issue where Concurrent Job Limit setting wouldn't persist on the General page
* Updated latest docker image to 7.1.4
* Updated PowerShell Universal PowerShell SDK to 7.1.4
* Fixed an issue where OpenID Connect login would result in a white screen
* Fixed an issue where visiting the Settings Configurations page would issue an app token
* Added Telemetry setting to General settings page
* Fixed an issue where the Reader role could see buttons they can't use.
* Fixed an issue where access control assigned privileges would show things they couldn't use.
* Fixed an issue where subscription licenses would show an invalid end date in the admin console
* Fixed an issue where subscription licenses would not show any information if they failed to activate
* Fixed an issue where PowerShell 7.0.x would not work with Universal
* Updated to Hangfire 1.7.25
* Fixed an issue loading the Pnp.PowerShell module in Universal
* Fixed an issue where Git sync could cause the server to fail to start
* Added documentation links to all pages.
* Fixed an issue where the security service could stop and not restart
* Fixed an issue where switching to the integrated environment for the security service would fail
* Fixed an issue where users without built in roles could view the admin console
* Fixed an issue where identities, roles, settings, published folders and rate limits limits could be viewed without reader access

## 2.2.1 - 8/10/2021

### Includes

* UniversalDashboard - v3.5.2
* UniversalDashboard - v2.9.9
* UniversalDashboard.Charts - 1.3.2
* UniversalDashboard.Map - 1.0
* UniversalDashboard.CodeEditor - 1.1.1
* UniversalDashboard.Style - 1.0.0

### Changed

#### Automation

* Fixed an issue where a default value of \[DateTime]::Now would cause the run script modal to show an error
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
* Fixed an issue where you couldn't delete the last item (Endpoints, scripts, dashboards, etc)
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
* Fixed an issue where jobs could restart (retry) even after running successfully

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

* Reverting a change made to status code pages (Unauthorized page) because it causes issues with SSO (Windows\WS-Fed\OIDC)

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
* Fixed an issue where standard (online) licenses would become inactive after some time
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

* Fixed an issue where string\[] types could not be used with ValidateSet attributes
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
Please see notes about [upgrading](getting-started/upgrading.md) from 1.x to 2.x
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
