---
description: Changelog for PowerShell Universal.
---

# Changelog

## 3.5.2 - 11/10/2022

#### APIs

* Fixed an issue where viewing the API page could result in a JavaScript error
* Fixed an issue where the bottom of API endpoint scripts could not be viewed.
* Fixed an issue where streams (warning, error, verbose, information) would cause APIs to throw an object reference exception.

#### Automation

* Add some more logging about job timeouts to help identify an issue with them.
* Fixed an issue where Get-PSUJobFeedback and Get-PSUJobParameter would not return data when using -Integrated
* Fixed an issue where parameter sets were not always correctly defined
* Fixed an UI issue with the schedule properties dialog

#### Dashboards

* Fixed an issue where -HideUserName didn't work on New-UDPage or New-UDDashboard when using Windows Authentication

#### Platforms

* Fixed an issue where the Agent environment wouldn't have a version.

## 3.5.1 - 11/9/2022

#### Dashboard

* Fixed an issue where certain -BaseURL would not render a dashboard

#### Platform <a href="#platform-4" id="platform-4"></a>

* Fixed an issue where online license keys would only partially install

## 3.5.0 - 11/8/2022

#### APIs

* Added the ability to view API info when One-Way git sync was enabled
* Added experimental feature for C#-based APIs
* Fixed an issue where data uploaded as files would be UTF8 encoded.
* Fixed an issue where folder view would not correctly create folders when over 3 parts
* Fixed an issue where changing an APIs URL would cause a 404
* Fixed an issue where testing an API with variables wouldn't return the specified values
* Added persistent API logging
* Fixed an issue where editing endpoint roles could result in the endpoint becoming inaccessible.

#### Automation

* Added the ability to view script info when One-Way git sync was enabled
* Added Git Sync trigger
* Fixed an issue where you could not view terminal instances
* Fixed an issue where terminal output could overwrite the prompt
* Fixed an issue where Warnings would overwrite the Failed error state of jobs
* Fixed an issue where terminating errors would cause job failures when Error Action was set to Continue
* Fixed an issue where jobs would not time out properly
* Fixed an issue where the Server Started trigger would run on the default job queue
* Fixed an issue where $UAJob.Parameters would be null
* User Profiles are now loaded by default when using run as credentials
* Added -DontLoadProfile to New-PSUSetting to disable loading of profiles for run as credentials
* Removed the limit on 25 jobs a day for the free version

#### Dashboard

* Added support for Read-Host
* Added support for Get-Credential
* Added support for $Host.UI.PromptForChoice
* Added support for Write-Progress
* Added Back button to advanced editor
* Added -TimeZone to New-UDDatePicker and New-UDTimePicker
* Fixed an issue where web socket JSON serialization would throw an error when referential loops were detected.
* Fixed an issue where New-UDDataGrid filters wouldn't render correctly when using a custom theme
* Fixed an issue where New-UDDataGrid row height would expand to its contents
* Fixed an issue where -PageSize wouldn't be honored on New-UDDataGrid
* Added -OnBlur to New-UDTextbox
* Added New-UDRating
* Fixed an issue where New-UDDatePicker\New-UDTimePicker would throw an error when invalid dates were typed
* Fixed an issue with the default color for New-UDButton
* Added -OnExport to New-UDDataGrid
* Fixed an issue where -LoadData on New-UDTable could cause errors when multiple tables were on a page

#### Platform

* Added support for specifying a custom favicon.ico
* Added Agent environment
* Added experimental feature support
* Licenses are now stored in the database
* Git manual mode is now the default
* Updated internal PowerShell Environment to 7.2.7
* Fixed an issue where links in the notification drop down would not work when hosted as a nested IIS site
* Admin Console Title now updates the brower's tab title
* Added the ability to limit users that can login to the admin console
* Fixed an issue where the app bar would be an incorrect color in dark mode on a custom login page
* Added scheduled and memory based environment recycling
* Improved the layout of modals in the admin console
* Git proxy type is set to auto instead of none by default to support git environment variables
* Fixed an issue where the MSI wouldn't correctly detect an existing appsettings.json file
* Fixed an issue where invalid git sync settings could cause heartbeats to retry continuously
* Improved validation on the git sync settings dialog
* Fixed an issue where changing a git remote with an external git client wouldn't update the local repo's remote
* Git sync now throws an exception if it cannot finish running a command in 60 seconds when using an external git client

## 3.4.6 - 11/2/2022

#### Platform

* Fixed an issue where online licenses could fail to activate

## 3.4.5 - 10/31/2022

#### Automation

* Fixed an issue where Verbose, Warning, and Error streams wouldn't produce a new line in the job log.

#### Platform

* Fixed an issue where running a process as a non-admin user in a domain environment could fail to start

## 3.4.4 - 10/25/2022

#### Automation

* Fixed an issue where default bool values would not be applied correctly when creating schedules
* Fixed an issue where schedules could be created with scripts that didn't exist

#### Platform

* Fixed an issue where user profiles for Run As credentials would not be loaded in some scenarios
* Fixed an issue where database connections could be leaked causing memory and transaction logs to grow
* Fixed an issue where invalid settings.ps1 files could cause the system to fail to load

## 3.4.3 - 10/20/2022

#### Pages

* Fixed an issue where forms couldn't display job output when using SQL persistence

#### Platform

* Added support for setting Git Manual Mode from appsettings.json (Data\GitManualMode = true)
* Fixed an issue where Set-PSUVariable -Integrated would throw an exception

## 3.4.2 - 10/19/2022

#### Automation

* Fixed an issue where jobs would timeout immediately

#### Dashboard

* Added -NavigationStyle to Get-UDTheme
* Fixed an issue where the dashboard logo would not be shown when using new themes
* Fixed an issue where UDCard with Avatar would have a small title text size
* Fixed an issue where dashboard navigation would reset when clicking navigation
* Fixed an issue where New-UDTimePicker would not return time in a consistent manner.

#### Pages

* Fixed an issue where invalid page files could cause other configuration files to fail to load
* Fixed an issue where text output type would not return a value

#### Platform

* Fixed an issue where Set-PSUVariable couldn't update a variable
* Fixed an issue where Get-PSUVariable -ValueOnly wouldn't return a deserialized value
* Fixed an issue where invalid settings.ps1 files could cause the server to not start
* Fixed an issue where Get-ChildItem would not return the value of a secret

## 3.4.1 - 10/16/2022

#### Dashboard

* Fixed an issue where -OnClick of New-UDChartJS wouldn't work

#### Platform

* Fixed an issue where the Configurations page would not update when creating\deleting items
* Fixed an issue where the service may fail to start if it doesn't have access to performance counter info (typically with IIS)
* Fixed an issue where the git sync service could start before PSU ready when using SQL persistence
* Fixed an issue with the SQL schema files
* Added support for not updating the SQL schema when starting the PSU service
* Added support for running the data migrator without install the schema
* Added support for continue running the data migrator even when there are errors

## 3.4.0 - 10/11/2022

#### API

* Fixed an issue where tags would not display in the admin console
* Fixed an issue where external -Path scripts would not be reloaded automatically.
* Added support for complex objects in param blocks within endpoints (PowerShell 7 only)
* Added Restart APIs button for administrators to restart the API processes.
* Fixed an issue where testing an endpoint in the admin console would not return when the endpoint returned an error

#### Automation

* Fixed an issue where old jobs could be left behind in SQL after a restart
* Added support for PSCredential parameters in Invoke-PSUScript
* Fixed an issue where long Read-Host messages would be cut off
* Added Windows Performance counters for Active Endpoints, Average Execution Time and Calls per second
* Fixed an issue where missing environments for APIs would cause all APIs to fail.
* The /api/v1/job/:id endpoint will now return parameters that were used to call the job
* Added schedule name to the job description
* Fixed an issue where a thread could run after a job had finished.
* Added support for dynamic default parameters for scripts
* Added the ability to view schedule parameters
* Added New User Login trigger
* STDOUT and STDERR will now be shown in the job log when running a process outside of the integrated environment.

#### Dashboard

* Added -AutoRefresh and -AutoRefreshInterval to New-UDTable
* Fixed an issue where the refresh button wouldn't be shown unless a title was specified in New-UDTable
* Added -Locale to New-UDTable
* Added -FilterDate to New-UDTableTextOption
* Fixed an issue where date filters wouldn't work properly
* Added -LoadTitle to New-UDPage
* Fixed an issue where New-UDDateTime wouldn't format dates properly due to missing time zone information
* Added Not Contains and Not Equals to New-UDDataGrid filters
* Added Windows Performance Counters for Active Connections
* Fixed an issue where -DefaultValue would not be returned with Get-UDElement and New-UDRadioGroup
* Added the ability to define a login page by using the base URL /login
* Added -Icon to New-UDSelect and New-UDSelectOption
* Fixed an issue where the comfortable option was mispelled for -Density on New-UDDataGrid
* Fixed an issue where New-UDDatePicker would switch between UTC and local time.
* Added -Avatar to New-UDCard and New-UDCardHeader
* Added -Action to New-UDCardHeader
* Added -LabelPlacement to New-UDSwitch

#### Pages

* Fixed an issue where the Forms fields page wouldn't navigate properly

#### Platform

* Added manual git sync mode
* Added maintenance mode for computers
* Added /api/v1/status endpoint to help support load balancer status codes
* Added support for detecting preview versions of PowerShell on Windows
* Fixed an issue where the T: translation provider wouldn't work with Get-Item
* Added support for accessing secret variables in configuration scripts
* Configuration scripts are now more resilient to non-terminating errors
* Fixed an issue where the DataMigrator tool could throw an Object Reference exception
* Added validation to prevent app tokens longer than 16 years expiration date
* Added a new option to the DataMigrator tool to delete the database before updating it.
* Changed the method of add the schema in the DataMigrator tool
* Added support for using a thumbprint for specifying a certificate.
* Fixed an issue where proxy settings would not be honored when using OIDC authentication

## 3.3.7 - 10/6/2022

#### Platform

* Fixed an issue where git sync would not honor HTTP proxy settings
* Fixed an issue where git sync could cause configuration issues on blank repositories.

## 3.3.6 - 9/27/2022

#### Dashboard

* Improved dashboard logging for when auto-deploy is enabled
* Fixed an issue where dashboards could hang when saving with syntax errors and auto-deploy was enabled

#### Platform

* Fixed an issue where jobs would not be groomed properly when using LiteDB
* Fixed an issue where identity detail tabs wouldn't change

## 3.3.5 - 9/22/2022

#### Automation

* Fixed an issue where execution time would be incorrect for running jobs

#### Platform

* Fixed an issue where many Groom jobs could be queued when groom jobs took some time to run
* Fixed an issue where git sync intervals over 59 seconds would cause the service to fail to start

## 3.3.4 - 9/20/2022

#### Automation

* Fixed an issue where the folder pane on the scripts page would not persist its size
* Fixed an issue where the View Script button would not be visible when using One-Way git sync

#### Dashboard

* Fixed an issue where New-UDTextbox -Mask would not accept RegEx.

#### Pages

* Fixed an issue where the Forms fields page wouldn't navigate properly

#### Platform

* Fixed an issue where git sync in git init Initialize mode using an external client would fail to properly set the origin branch
* Fixed an issue where git status would be marked as failed after service restart

## 3.3.3 - 9/17/2022

#### Platform

* Fixed an issue where git sync would fail occasionally on multi-node installs using SQL
* Fixed an issue where desktop mode would show a login page

## 3.3.2 - 9/16/2022

#### Automation

* Fixed an issue where job run time would not be shown for jobs that didn't succeed
* Fixed an issue where string\[] parameter values would not show on the jobs page
* Increased Hangfire job timeout for LiteDB from 24 hours to 14 days.
* Fixed an issue where calling Invoke-PSUScript in integrated mode wouldn't set the user name of the caller
* Fixed an issue where job output may not immediately be shown once it completed. It would state that the job didn't have any output
* Fixed an issue where Get-PSUJobPipelineOuput -Integrated would throw an exception on failed jobs
* Fixed an issue where child and triggered jobs wouldn't show up in the Script \ Jobs tab

#### Dashboard

* Fixed an issue where New-UDTreeView wouldn't work properly when combining -Node with -OnNodeClicked
* Added missing Title plugin for New-UDChartJS
* Fixed an issue where 2 data grids on one page would cause rendering to fail
* Fixed an issue where a runspace would leak when saving changes with AutoDeploy leading to high memory usage. Much worse when using VS Code, the PSU extension and file.autoSave = afterDelay
* Fixed an issue where ScriptBlocks could be serialized from dashboards causing rendering issues

#### Platform

* Fixed an issue where git sync may not run due to the time zone and git sync interval
* Fixed an issue where duplicate computers could be listed in Platform \ Computers
* Fixed an issue where the heartbeat service would not run on each node properly
* Fixed an issue where identites would be stored in demo mode
* Fixed a display issue with the Settings \ General page
* Fixed an issue where git sync with an external client in init mode would throw the error: Git Error: error: unknown switch \`M'
* Fixed an issue where proxy settings would not work for proxies without credentials

## 3.3.1 - 9/14/2022

#### Dashboard

* Fixed an issue where line charts with New-UDChartJS would throw an error
* Fixed an issue where New-UDMonitor would not render
* Fixed an issue where the page size wouldn't successfully change with New-UDDataGrid

#### Automation

* Fixed an issue where job output would be a single line

#### Platform

* Fixed an issue where the git settings modal would reset after 5 seconds
* Fixed an issue where git sync configured for the first time through the admin console would state a sync was running but never finish
* Fixed an issue where groom jobs could queue indefinitely if one was process for a long time

## 3.3.0 - 9/13/2022

#### Breaking Change

* The UniversalDashboard module is no longer distributed as a separate module and all features are now in the Universal module.

#### APIs

* Endpoint URLs are now trimmed of white space during creation or update
* Added support for editing endpoint paths in the UI
* Added support for editing endpoints with paths in the UI

#### Automation

* Added LocalIpAddress, RemoteIpAddress, LocalPort and RemotePort to the event data sent to the User Logon trigger
* Script right hand panel will now persist the last selected tab on the right hand side and use that as default
* Fixed an issue where terminal instances could fail to start
* Added support for executing a job on a specific computer in the cluster
* Added Write-PSUError to output errors to the Errors tab without causing errors in the script
* Errors in the Errors tab now include stack traces
* Fixed an issue where an error would be shown multiple times in the Errors tab
* Fixed an issue where string\[] parameters would not show the correct type of select control
* Fixed an issue where job output wouldn't be completely visible
* Added support for passing files as parameters to jobs
* Increased the number of hangfire workers to 100
* Fixed an issue where schedules wouldn't always register correctly with Hangfire
* Fixed an issue where schedules would equate when they were not equal causing problems managing similar schedules
* Added support for running schedules on demand
* Fixed an issue where exit commands could be issued through a terminal
* Fixed an issue where PSFramework logging output would be poorly displayed in PSU
* Name is now a required property for schedules
* Added support for scheduling scripts on a specific computer or all computers.
* Fixed an issue where a misconfigured user login trigger could cause logins to fail
* Fixed an issue where scripts would not be displayed on jobs when not logged in as administrator

#### Dashboard

* Added data-theme attribute to the HTML tag to allow for adaptive CSS styles
* Added -Sx to New-UDTypography to be able to apply theme-based styles
* Added Get-UDElement support to New-UDGridLayout.
* Added -LoadDetailContent to New-UDDataGrid.
* Fixed an issue where dashboard logging of Write-\* cmdlets would stop working when auto-deploy was enabled and a change was made
* Added -BorderWidth to New-UDChartJS
* Added -OnEdit to New-UDDataGrid
* Added all colors to New-UDChip
* Updated to ChartJS v3.9.1
* Increased button size on dashboard page
* Fixed an issue where OnRowExpand in New-UDTable was statically set to colspan 6
* Fixed an issue where -DefaultValue would not be present in forms or steppers when using New-UDRadioGroup
* Fixed an issue where New-UDTextbox with a mask wouldn't not accept enter to submit a form
* Added -Href to New-UDListItem to support easier custom navigation
* Fixed an issue where field names were case-sensitive for New-UDDataGrid
* Added Wildcard support to Find-UDIcon
* Fixed an issue where -HideUserName was always on when using New-UDDashboard and -Content
* Fixed an issue where New-UDDataGrid would not properly render rows.
* Added icon search to the dashboard editor
* Added missing icons
* Fixed an issue where New-UDAutoComplete would show a react error when removing the selected item
* Added bubble chart support to New-UDChartJS
* Fixed an issue where -RowsMax was not honored on New-UDTextbox
* Added support for specifying any component in New-UDListItem -Label
* Fixed an issue where dynamic UDTreeViews would stop working when collapsing them
* Added -Expanded to New-UDTreeView and New-UDTreeNode
* Fixed an issue where filters would be lost when changing pages in New-UDDataGrid
* Fixed an issue where hidden columns would reappear when performing any action in the New-UDDataGrid
* Fixed an issue where -Content of New-UDTypography would not do anything
* Fixed an issue where -ClassName was not applied in New-UDTable and New-UDSelect
* Fixed an issue where not all languages would work with New-UDDataGrid
* Added -Locale to New-UDDateTime
* Added the $DashboardName built-in variable
* Fixed an issue where the default header would be shown before the page was loaded.

#### Pages

* Fixed an issue where words would not wrap in a card
* Fixed an issue where tables would not scroll and would extend out of their container

#### Automation

* Navigating back to the scripts page will open the folder that you previously had open

#### Platform

* Added sorting to the tags page
* Added Demo mode.
* Fixed an issue where Get-PSUScript -Tag would throw an exception.
* Added builds for Windows 10+ ARM64.
* Fixed an issue where the groom service would throw exceptions while grooming jobs
* Loading screen is now shown during service startup
* Added support for Initialization script
* Fixed an issue where the access control page could create access controls with invalid parameters for the parameter sets
* Improved the UI to prevent queuing a git sync if one is already running
* Improved the UI to display when a git sync is running
* Manual git syncs now ignore the git sync interval setting
* Fixed an issue where calling /api/v1/apptoken/:id as an administrator wouldn't allow you to view all tokens
* Fixed an issue where calling /api/v1/apptoken/:id as a non-administrator could access other app tokens
* Fixed an issue where array variables could not be created in the admin console
* Added Uptime to home page
* Added header forwarding
* Added support for using an external git client when using git sync

## 3.2.8 - 8/29/2022

#### Dashboards

* Fixed an issue where New-UDChip would not render properly

## 3.2.7 - 8/27/2022

#### Dashboards

* Fixed an issue where New-UDDataGrid column rendering would not work properly
* Fixed an issue where -HideUserName on New-UDDashboard did not work properly

## 3.2.6 - 8/24/2022

#### Platform

* Fixed an issue where the first time git sync was setup, the admin console could display a JavaScript error
* Fixed an issue where the git sync interval setting would not be honored correctly when multiple nodes were connected
* Fixed an issue where git sync would fail to load configuration properly when initializing using clone mode

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
