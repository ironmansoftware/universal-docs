---
description: Changelog for PowerShell Universal.
---

# Changelog

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
