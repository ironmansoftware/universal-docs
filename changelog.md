---
description: Changelog for PowerShell Universal.
---

# Changelog

## 4.1.2 - 9/25/2023

#### Apps

* Fixed an issue where -OnLoading of New-UDPage would not have an affect
* Fixed an issue where New-UDElement would leak event handlers (#2692)

#### Automation

* Fixed an issue where saving scripts would be slow if there were many scripts defined

#### Platform

* Fixed the default connection string in the MSI to work with SQLite.
* Fixed an issue with viewing log entries in the admin console when using SQLite.

## 4.1.1 - 9/18/2023

#### Apps

* Fixed an issue where the admin link would not work properly in a nested IIS site (#2672)
* Fixed an issue where Get-UDElement would display errors when a property did not exist instead of returning $null
* Fixed an issue where the date picker would not be visible in dark themes (#2669)
* Fixed an issue where PromptForChoice wouldn't behavior properly when run twice on the same page

#### APIs

* Fixed aan issue where Send-PSUEvent hub did not work out of the integrated environment (#2674)

#### Platform

* Fixed an issue where certain roles would forward to a missing page rather than the admin console

## 4.1.0 - 9/12/2023

#### APIs

* Added Get-PSUEventHubConnection
* Added -ConnectionId to Send-PSUEvent
* Send-PSUEvent can now return data when using -ConnectionId

#### Apps

* Adding BackgroundImage and BackgroundRepeat to New-UDPage (#2325)
* Adding Disabled to New-UDSelectOption (#2491)
* Adding md to Size to New-UDIcon (#2528)
* Added -Label to New-UDProgress (#2553)
* Added -OpenInNewWindow to New-UDListItem (#2540)
* Added -Minimum and -Maximum to New-UDTextbox (#2455)
* Fixing issues with Show-UDToast -MessageSize (#1000)
* Fixing issues with Show-UDToast -Icon (#1913)
* Added additional configuration options to apps in the admin console
* Added Show-UDSnackbar\Hide-UDSnackbar (#2561)
* Fixing issue with New-UDDataGrid pagination (#2546)
* Fixed an issue where row selection in New-UDDataGrid wasn't available in Get-UDElement (#2573)
* Added -OnSelectionChanged to New-UDDataGrid
* Fixed an issue where schema forms -OnSubmit would not run
* Added -DefaultSortColumn and -DefaultSortDirection to New-UDDataGrid (#2011)
* Fix issue with min\max on New-UDDatePicker (#2580)
* Fixed an issue with New-UDSwitch -LabelPlacement should be start not left (#2601)
* Added Restart and Admin Console links to dashboards of admins (#2362)
* Added Get-UDTheme -Current (#2508)
* Fix New-UDAutocomplete to look at options for defaults (#2583)
* Added -ArgumentList to Sync-UDElement (#1815)
* Clear autocomplete with Set-UDElement (#2631)
* Fixed an issue where row selection wouldn't always work when filtering with New-UDTable (#2630)
* Added -Disabled to New-UDAutocomplete (#2639)
* Fixed an issue where links in New-UDMarkdown didn't follow the theme (#2296)
* Added $TimeZone variable to apps (#2646)
* Added missing New-UDAutoCompleteOption to live docs (#2640)
* Power Managing a dashboard will now do so on all nodes when using SQL Server (#1360)
* Fixed an issue where the nivo chart docs were not present on the live docs (#2640)
* Fixed an issue with -CirclePacking and -TreeMap in New-UDNivoChart
* Fixed an issue with -Heatmap in New-UDNivoChart
* Added New-UDTheme (#2653)
* Fixed an issue where several components (tables, pickers, charts) would not update when using within a UDDynamic (#2661)
* Improved the behavior of New-UDButtonGroup (#2651)
* Fixing issue with New-UDAvatar -Variant not supporting default round (#2633)
* Fixed an issue where New-UDUpload did not work in a nested IIS site (#2657)
* Fixed an issue where autocomplete would fail to render if it was pass a single value that wasn't an array (#2668)

#### Automation

* Added Error status for jobs that succeed but have errors
* Added a Create Scheduled button to the Scripts \ Schedules tab. (#2541)
* Added support for cmdlets in -Command in New-PSUScript (#2605)
* Fixed an issue with editing schedules in the admin console (#2659)

#### Platform

* Add configurable git sync timeout (#2466)
* Added git to the linux docker container (#2472)
* Updated the integrated and agent environments to 7.3.6 (#2494)
* Administrator role now defaults to $false (#2492)
* Added a Run Module Discovery button to the module page (#2486)
* Added $RefreshToken to access the OIDC refresh token
* Added support for SQLite
* Updated to Microsoft.Data.SqlClient version 5.1.1
* Added loaded Assemblies to the process view
* Added additional branding settings
* Added Remove-PSUCache
* Added ModuleDiscoveryFrequency to Set-PSUSettings (#2595)
* Added Get-PSUPublishedFolder (#2622)
* Added SystemLogLevel to appsettings.json
* Fixed an issue where the default theme setting would not take effect (#2292)
* The secret variable credential dialog now suggests including the domain in the user name (#2625)
* Fixed an issue where Grant-PSUAppToken would generate tokens with invalid roles besides the first role specified.
* Fixed an issue where modules in the Modules directory were imported into the PSU server during startup
* Fixed an issue with editing modules when a Universal extension module was installed
* Fixed an issue where readonly resources could show up in configuration files
* Added support for PSScriptAnalyzer settings files (#2658)
* Fixed an issue where the module REST API did not work with app tokens.

## 4.0.12 - 8/31/2023

#### Automation

* Fixed an issue where scripts provided by modules would not be visible in folder view
* Fixed an issue where job output could be malformed when storing in SQL causing an error in the admin console (#2644)

## 4.0.11 - 8/28/2023

#### APIs

* Endpoints will now attempt to read form data even if the HTTP client doesn't specify a Content-Type header (#2612)
* Fixed an issue where authenticated event hub clients would not receive events.

#### Apps

* Fixed an issue where the app designer would add 2 IDs when the ID of a component was changed (#2589)
* Fixed an issue where the default choice for PromptForChoice would throw an exception (#2607)
* Fixed an issue where Get-UDPage would throw an exception if the page was not found causing the entire app to fail to load (#2610)
* Fixed an issue where UDTreeView selected items were not visible in the default dark theme (#2613)
* Fixed an issue where expired tokens would cause -GrantAppToken to fail to generate a new token
* Fixed an issue where recursive object paths could cause an app crash (#2627)
* Fixed an issue where -OnLoadOptions and -Multiple wouldn't show selections in New-UDAutocomplete (#2604)
* Added -Options to New-UDTableColumn (#1097)
* Fix New-UDAutocomplete to look at options for defaults (#2583)

#### Pages

* Fixed an issue where unauthenticated pages would clear out the form data after 3 seconds (#2611)

#### Platform

* Fixed an issue where no error was shown when there was a failure to save a translation file (#2618)
* Fixed an issue where database git sync could run into an OutOfMemory exception (#2620)
* Fixed an issue where an exception was thrown while attempting to groom an expired apptoken that was used by a job (#2621)
* Added universal-modules docker image tag (#2624)
* Added Download System Logs button
* Implemented a database recovery feature if the LiteDB database is corrupted
* Resources are now marked readonly in the admin console (#2587)
* Fixed an issue where variables with a role wouldn't show up for admins unless it had the Administrator role
* Fixed an issue with the log viewer not retaining filters when sorting or paging.
* Fixed an issue with the documentation links in the admin console

## 4.0.10 - 8/14/2023

#### APIs

* Fixed an issue where specifying an invalid environment could cause multiple API to fail to load. Now falls back to integrated and shows a warning (#2591)

#### Apps

* Fix issue with min\max on New-UDDatePicker (#2580)
* Fixed an issue where the MUI X license key was expired
* Fixed an issue with New-UDSwitch -LabelPlacement should be start not left (#2601)
* Breaking: Query string values are now passed in via a $Query dictionary rather than as variables to avoid potential injection issues

#### Automation

* Added -PreformattedJobOutput to Set-PSUSettings to improve performance of large job output

#### Pages

* Fixed an issue where default values for form textboxes didn't work (#2592)

#### Platform

* Fixed an issue where deleted computers could be displayed in the Run As dropdown (#2593)
* Fixed an issue where 1 day rate limits would actually define a 24 day rate limit (#2594)
* Fixed an issue where canceling a git edit with a missing repo directory would fail (#2599)
* Fixed an issue where TCP and UDP logging targets would not configure properly through the admin console (#2600)
* Fixed an issue where app tokens set to never expire would not authenticate properly (#2598)

## 4.0.9 - 7/30/2023

#### APIs

* Fixed an issue where the event hub edit modal would be empty
* Fixed an issue with connecting to event hubs that had authentication but did not specify roles

#### Apps

* Fixed an issue adding images to the app designer
* Fixing issue with New-UDDataGrid pagination (#2546)
* Fixed an issue where row selection in New-UDDataGrid wasn't available in Get-UDElement (#2573)
* Added -OnSelectionChanged to New-UDDataGrid
* Fixed an issue where schema forms -OnSubmit would not run

#### Automation

* Job output is now set at verbose for the log level to avoid duplicating the output in the database by default to avoid performance issues. Job output is still logged to the job output tables.

#### Platform

* Fixed an issue where the access control and app token dialog would not allow edits (#2576)
* Fixed an issue where the home page of the admin console could show a JavaScript error if the health checks failed to return a value (#2575)

## 4.0.8 - 7/23/2023

#### Automation

* Fixed an issue where rerun job would not populate string array parameters correctly. (#2434)
* Fixed an issue where rerun job would not select the correct parameter set

#### Apps

* Fixed an issue where New-UDTickPicker didn't display the picker component (#2551)
* Fixed an issue where New-UDToolTip didn't have a -Type parameter
* Fixed an issue where New-UDAutoComplete would display the value rather than the name of New-UDAutoComplete option when using -OnLoadOptions
* Fixed an issue where the export and delete logging buttons would not work for nested IIS sites (#2554)
* Fixed an issue where -Scrollable on didn't work on New-UDTabs (#2557)
* Fixed an issue where -Size for New-UDButton didn't display properly on the live docs (#2462)
* Fixed an issue where Get-UDElement would return an invalid value from New-UDAutoComplete
* Fixing issues with Show-UDToast -MessageSize (#1000)
* Fixing issues with Show-UDToast -Icon (#1913)
* Fixed a JavaScript error in the App Designer
* Fixed an issue where boolean parameters would not be serialized properly by the app designer (#2562)
* Fixed an issue where templates wouldn't work on Linux due to case sensitivity
* Fixed visual issues with textbox and autocomplete (#2419)

#### Platform

* Published folders now set the Cache-Control and Last-Modified headers
* Fixed an issue with creating and edit roles in the admin console (#2563)
* Fixed a concurrency issue with $Cache scope (#2564)

## 4.0.7 - 7/17/2023

#### Automation

* Fixed an issue where the Run Script button could throw a JavaScript error in the admin console

#### Platform

* Fixed an issue where the role selector would not populate in some circumstances in the admin console (#2545)
* Fixed an issue where environments would disappear if clicking cancel in manual git sync when no environments.ps1 file was defined.
* Fixed an issue where read only items (PSUHeader) would be recreated when adding new items to the same config file (#2454)
* Fixed an issue where read only items would have edit and delete buttons in the admin console
* Updated to Microsoft.Identity.Client 4.54.1 to support Pnp.PowerShell 2.2.0

## 4.0.6 - 7/11/2023

#### Platform

* Fixed an issue where X-Forwarded headers were not processed correctly by the Kestrel server when a remote reverse proxy was used.
* Added -LogGroomDays to Set-PSUSetting
* Fixed an issue where log messages would not be groomed properly
* Fixed an issue where the LiteDB database could become corrupt after some time when running in Azure using Azure File Shares.

#### Apps

* Fixed an issue where -Height on New-UDCodeEditor wouldn't have an affect (#2525)
* Adding md to Size to New-UDIcon (#2528)
* Fixed an issue with -Options in New-UDChartJS wouldn't apply properly
* Fixed an issue where saving an app page would return a 500 error (#2531)
* Fixed an issue that was causing the App Live Docs to display an error toast on some pages.

## 4.0.5 - 7/6/2023

#### Automation

* Fixed an issue with One Time schedules and boolean parameters

#### Platform

* Fixed an issue with PSModulePath in external PowerShell hosts.
* Fixed an issue where Format On Save would throw an exception when removing the last item in a collection
* Fixed an issue starting external PowerShell processes when running as Local System and no alternate credentials are specified.

## 4.0.4 - 7/4/2023

#### Apps

* Fixed an issue where Get-UDPage wouldn't work on Linux

#### Automation

* Fixed an issue where running scripts as alternate users could result in an error about Out-PSUPipeline not being found.

#### Platform

* Fixed an issue where the logging system would fail to initialize if the SystemLogPath value was not set.
* Fixed an issue where running processes as alternate users would require the SeTcbPrivilege in some environments (#2521)

## 4.0.3 - 7/2/2023

#### Apps

* Fixed an issue where New-UDChartJS would not fill a line chart when a dataset was used by default
* Fixed an issue where the page editor would jump to the top on save (#2502)
* Fixed an issue where custom FavIcon would not load from URLs

#### Automation

* Fixed an issue where Invoke-PSUScript did not work with SecureStrings.
* Fixed an issue where the System Default time zone would cause One-Time schedules to display the wrong time in the admin console (#2495)
* Fixed an issue where unauthenticated event hubs would not connect properly
* Fixed an issue where terminals could not be started when One-Way git sync was enabled (#2504)
* Fixed an issue where schedules could not be deleted
* Fixed an issue where One-Time schedules created with New-PSUSchedule would have parameters double serialized (#2500)
* Fixed an issue where the Job Diagnostics button wouldn't redirect to the correct page in a nested site (#2506)

#### Platform

* Fixed an issue where navigating to the PowerShell Universal Modules list would throw a JavaScript error on the modules page.
* Cookies are now prefixed with the base URL to allow for different sessions to the same host running multiple PSU instances
* Fixed an issue with creating logging targets in the admin console
* Fixed an issue where loading multiple apps from a module would fail and only load the first app (#2511)

## 4.0.2 - 6/25/2023

#### APIs

* Fixed concurrency issues when adding or removing APIs
* Fixed an issue where API docs would not work if authentication was enabled but no roles were defined.

#### Automation

* Fixed an issue where Job Handshake Timeout was not being set properly (#2476)
* Fixed an issue with editing scripts with tags (#2489)

#### Apps

* Button shouldn't default text to button (#2468)
* Fixed an issue where the code editor would switch to light theme when updated (#2477)
* Fixed an issue where the code editor wouldn't resize when the window resized (#2478)
* Fixed an issue where autocomplete would break once a value was selected and navigated away when using name\value in New-UDAutoCompleteOption
* Fixed an issue where the default ChartJS line chart wasn't filled or have any tension applied to the line
* Fixed an issue where New-UDLink -Children would not render properly (#2490)
* Removed default card title and text
* Designer: Fixed an issue where the code view wouldn't display anything
* Designer: Fixed an issue where editing an icon would throw a JavaScript error
* Designer: Fixed an issue where the component resize handles were not visible in dark mode
* Designer: Added fields for component positioning.
* Designer: General fixes and improvements to the property and layout editor

#### Pages

* Fixed an issue where pages would not display correctly.

#### Platform

* Fixed an issue where external app token validation did not work.
* Fixed an issue where Set-PSUVariable would not update secret values (#2475)
* Rolled back a change that set the PSModulePath on startup that was causing unexpected behavior
* Fixed an issue where git mode would always be Manual if configured from appsettings.json
* Fixed an issue where the heartbeat job would retry indefinitely in the event of a failure and fill up the hangfire job queue
* Fixed an issue where the roles drop down was empty (#2483)
* Fixed an issue where searching for modules would throw an exception in the admin console
* Fixed an issue where the module action buttons were obscured by the module name
* Added support for specifying a license via environment variable

## 4.0.1 - 6/14/2023

#### Apps

* Fixed an issue where ChartJS would not display data properly (#2463)
* Fix small size for switch (#2354)
* Fixed an issue where apps with -Component parameters would not load properly (#2458)

#### Automation

* Fixed an issue with viewing scripts in folders (#2418)
* Fixed an issue with folders when a module was installed via the admin console

#### Platform

* Fixed an issue where log entry time stamps were not displayed correctly (#2460)
* Fixed an issue where Demo mode wouldn't display the default dashboard correctly (#2461)
* SameSite=None cookies are now optional
* Fixed an issue where accessing PSU remotely would not work with some browsers

## 4.0.0 - 6/13/2023

#### API

* API endpoint documentation now only shows endpoints the user has access to (#363)
* Added Event Hubs

### Apps

* Replaced react-tooltip with MUI tooltip
* Added -Sx, -Arrow, -FollowCursor, -EnterDelay, -LeaveDelay to New-UDTooltip
* Removed -Type and -Effect from New-UDTooltip
* Added -Truncate to New-UDTypography
* Added New-UDBreadcrumbs (#2150)
* Added support for validation, help text and display messages to New-UDForm -Script (#2043)
* Added -ShowBackButton to New-UDForm -Script (#2044)
* Added -ShowSearch to New-UDTransferList (#2340)
* Fixed an issue where $EventData -OnEdit in New-UDDataGrid would be a string (#2071, #2070, #1978)
* Removed -PopOut from New-UDExpansionPanelGroup (#2373)
* Fixed -Type Accordion on New-UDExpansionPanelGroup (#2373)
* Removed New-UDCodeEditor -Autoresize and set the default to autoresize (#2146)
* Added -Dense to New-UDAlert (#2214)
* Added New-UDButtonGroup and New-UDButtonGroupItem (#2180)
* Added -HelperText to New-UDTextbox (#2285)
* Added -OnChange to New-UDTextbox (#2287)
* Added -Content and Content parameter set to New-UDIcon (#640)
* Added New-UDHelmet
* Added GitHub-Flavored Markdown to New-UDMarkdown
* Added App Designer
* Added Test-UDConnected
* Added -NoData to New-UDTableTextOption (#2112)
* Added -JustifyContent to New-UDStack (#2189)
* Added the ability to disable session time out (#296)
* Added -Width and -Height to New-UDTransferList (#1452)
* Added New-UDDataGridColumn (#2258)
* Added Out-UDDataGridData (#2266)
* Added New-UDSpeedDial and New-UDSpeedDialAction (#2157)
* Added -Dense to New-UDList (#2300)
* Added -Dense to New-UDAlert (#2214)
* Added New-UDButtonGroup and New-UDButtonGroupItem (#2180)
* Added -HelperText to New-UDTextbox (#2285)
* Added -OnChange to New-UDTextbox (#2287)
* Apps now start asynchronously on server startup
* Fixed issue with New-UDAppBar -Footer (#2176)
* Remove support for Universal Dashboard Marketplace
* Renamed Dashboards to Apps
* Theme is now persisted per app (#2156)
* Fixed an issue where New-UDListItem -Label couldn't be a number (#2107)
* Added cursor pointer to Nivo charts with onClick handlers

#### Automation

* Breaking: One Time schedules are no longer written to schedules.ps1
* Added support for SecureString parameters (#1467)
* Added support for markdown in script descriptions (#2128)
* Added -Queue to Invoke-PSUScript
* Added support for IValidateSetValuesGenerator (#472)
* Script page now uses tabs for each section (#551)

#### Platform

* Added support for nested roles (#2442)
* Added Claim Type and Value autocomplete (#2201)
* Added Roles to secret variables (#2350)
* Added support for setting the Content-Security-Policy header (#2395)
* Added support for wildcard subdomains in CORS (#2408)
* Added --appsettings and --windowTitle to desktop mode
* Added buttons to run, clear and refresh health checks.
* Added -HideRunOn and -HideEnvironment to Set-PSUSetting (#2294)
* Added -Truncate Disables text wrapping and adds ellipsis for overflow (#2332)
* Fixed an issue where docker images would not run properly (#2359)
* Added groom job health check (#1839)
* Added export button for logs (#2318)
* Added Database (LiteDB and SQL), UDP, TCP and HTTP logging targets
* Added log viewer in admin console
* Added PSScriptAnalyzer and forwardWindowsAuthToken health checks
* Added -Reset to Sync-PSUConfiguration
* Added Suspend-PSUFileWatcher and Resume-PSUFileWatcher
* Added -Module, -Command to New-PSUApp
* Added -Module, -Command to New-PSUScript
* Added -Module, -Command to New-PSUEndpoint
* Added support for loading resources from modules.
* Added Health Checks
* Added LastUsed property to AppTokens (#2173)
* Added -LogoutUrl to OIDC (#764)
* Added -Credential to Environments (#1683)
* Added middleware.ps1
* Added logging header (#2286)
* Updated to PowerShell 7.3.1
* Updated to .NET 7.0.102
* Removed PowerShell Protect support.
* Removed templates
