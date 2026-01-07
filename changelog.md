---
description: Changelog for PowerShell Universal.
---

# Changelog

## 5.6.13 - 01/07/2026

### Security Fix

* \[CVE-2026-0618] - Apps - Show-UDToast -Message and -Title are now HTML encoded to prevent XSS attacks.

### Bug Fixes

* Admin Console - Fixed an issue where Upload and Import scripts were visible when the console was in read-only mode.
* Agent - Fixed agent memory leak when using Windows PowerShell compatibility mode. [#5475](https://github.com/ironmansoftware/powershell-universal/issues/5475)
* Git - Takeown Fails with syntax error on some operating systems [#5470](https://github.com/ironmansoftware/powershell-universal/issues/5470)
* Module - Added -UseBasicParsing to Invoke-WebRequest calls in the Universal module
* Platform - Fixed an issue viewing files in published folders that use an absolute path [#5485](https://github.com/ironmansoftware/powershell-universal/issues/5485)

## 5.6.12 - 12/11/2025

### Bug Fixes

* Admin Console - Order Deployments by reverse chronological order (newest at the top) [#5401](https://github.com/ironmansoftware/powershell-universal/issues/5401)
* Admin Console - Logging viewer displays timestamps ahead of actual time (double conversion under en-AU / Hobart) [#5370](https://github.com/ironmansoftware/powershell-universal/issues/5370)
* Admin Console - Schedules “Next Execution” and Home cards ignore browser locale (en-AU) and show MM/DD/YYYY [#5369](https://github.com/ironmansoftware/powershell-universal/issues/5369)
* Admin Console - Parameter list does not appear in task scheduler [#5405](https://github.com/ironmansoftware/powershell-universal/issues/5405)
* Admin Console - Deployments do not include prerelease tag [#5399](https://github.com/ironmansoftware/powershell-universal/issues/5399)
* Admin Console - Fixed an issue with the favicon not displaying on the login page [#5437](https://github.com/ironmansoftware/powershell-universal/issues/5437)
* Admin Console - Added toggle switch for condensed job table view [#5432](https://github.com/ironmansoftware/powershell-universal/issues/5432)
* Admin Console - Added missing Restart APIs button [#5450](https://github.com/ironmansoftware/powershell-universal/issues/5450)
* Admin Console - Added the ability to create endpoints by Module and Command [#5443](https://github.com/ironmansoftware/powershell-universal/issues/5443)
* APIs - Having using namespace at top of script prevent document from processing [#5424](https://github.com/ironmansoftware/powershell-universal/issues/5424)
* APIs - Swagger includes standard cmdlet parameters [#5423](https://github.com/ironmansoftware/powershell-universal/issues/5423)
* Apps - MUI X Expired package version [#5410](https://github.com/ironmansoftware/powershell-universal/issues/5410)
* Apps - New-UDLink child icons break in v5.6.11 [#5427](https://github.com/ironmansoftware/powershell-universal/issues/5427)
* Apps - New-UDMap -ZoomControlPosition is ignored [#5412](https://github.com/ironmansoftware/powershell-universal/issues/5412)
* Apps - Fixed an issue with New-UDTextbox -Mask and other parameters [#5407](https://github.com/ironmansoftware/powershell-universal/issues/5407)
* Automation - Reduced default Hangfire worker count to avoid PostgreSQL connection exhaustion [#5391](https://github.com/ironmansoftware/powershell-universal/issues/5391)
* Automation - Improved VS Code mode file change detection performance for scripts [#5417](https://github.com/ironmansoftware/powershell-universal/issues/5417)
* Git - Prevent Git Credential Manager from prompting for credentials
* Git - Improve error reporting when Git operations fail
* Git - Add support for disabling timed git sync [#5360](https://github.com/ironmansoftware/powershell-universal/issues/5360)
* Git - Fixed an issue using SSH keys [#5434](https://github.com/ironmansoftware/powershell-universal/issues/5434)
* Installer - 5.6.11 MSI install asked me if I wanted server or desktop install [#5418](https://github.com/ironmansoftware/powershell-universal/issues/5418)
* Platform - Cannot import/declare module configuration by name [#5400](https://github.com/ironmansoftware/powershell-universal/issues/5400)
* Platform - Improved performance of groom job [#5435](https://github.com/ironmansoftware/powershell-universal/issues/5435)
* Platform - Fixed an issue with psu.exe database migrations to SQL Server
* Platform - Fixed an issue calling Connect-AzAccount
* Module - Invoke-PSUEndpoint not returning errors [#5411](https://github.com/ironmansoftware/powershell-universal/issues/5411)
* Module - Fixed an issue calling Invoke-PSUScript with -Integrated and -Wait
* Module - Improved performance of Wait-PSUJob

## 5.6.11 - 11/19/2025

### Bug Fixes

* Admin Console - Issue with creating app tokens [#5379](https://github.com/ironmansoftware/powershell-universal/issues/5379)
* Admin Console - Improved git settings credential dialog [#5364](https://github.com/ironmansoftware/powershell-universal/issues/5364)
* Platform - File System Watcher in 5.6.x does not respect module changes [#5385](https://github.com/ironmansoftware/powershell-universal/issues/5379)
* Platform - Fixed an issue where SQLite VACUUM would run too frequently. [#5402](https://github.com/ironmansoftware/powershell-universal/issues/5402)
* Module - Invoke-PSUScript errors in strict mode [#5339](https://github.com/ironmansoftware/powershell-universal/issues/5339)

## 5.6.10 - 11/12/2025

### Bug Fixes

* Admin Console
  * Nested jobs table should be more condensed [#5328](https://github.com/ironmansoftware/powershell-universal/issues/5328)
  * Parameterized variables do not repopulate when rerunning a job [#5313](https://github.com/ironmansoftware/powershell-universal/issues/5313)
  * Variables not visible when created from module [#5314](https://github.com/ironmansoftware/powershell-universal/issues/5314)
  * Elapsed timer loops for long running jobs [#5306](https://github.com/ironmansoftware/powershell-universal/issues/5306)
  * Variables - Don't show the "Disable run as support" for string types for the secret [#5344](https://github.com/ironmansoftware/powershell-universal/issues/5344)
  * A duplicated schedule breaks Scheduling [#5343](https://github.com/ironmansoftware/powershell-universal/issues/5343)
  * Pending changes in the UI should prompt if clicking away from popup [#5349](https://github.com/ironmansoftware/powershell-universal/issues/5349)
  * Modifying existing tag hangs the UI [#5346](https://github.com/ironmansoftware/powershell-universal/issues/5346)
  * UI becomes unresponsive after saving changes to an existing app settings [#5274](https://github.com/ironmansoftware/powershell-universal/issues/5274)
* APIs
  * Fixed an issue with APIs returning blank values when provided by a module
  * OpenAPI spec omits endpoints with Role after IIS recycle when the documentation has Authentication enabled [#5345](https://github.com/ironmansoftware/powershell-universal/issues/5345)
  * Send-PSUEvent: second send to same Hub/ConnectionId intermittently fails; Get-PSUEventHubConnection -Active sometimes omits active connections [#5295](https://github.com/ironmansoftware/powershell-universal/issues/5295)
* Apps
  * App logging is now too verbose [#5342](https://github.com/ironmansoftware/powershell-universal/issues/5342)
  * New-UDLink with no text shows as "Ironman Software" [#5294](https://github.com/ironmansoftware/powershell-universal/issues/5294)
  * Editing App pages in Docker results in 404 [#5357](https://github.com/ironmansoftware/powershell-universal/issues/5357)
  * Disable Interactive Host also disables write-host logging [#5352](https://github.com/ironmansoftware/powershell-universal/issues/5352)
* Automation
  * Fixed an issue loading parameters from scripts in a module
  * RBAC issue with viewing job from /automation/scripts [#5340](https://github.com/ironmansoftware/powershell-universal/issues/5340)
  * Pester / Tests page not showing any scripts [#5312](https://github.com/ironmansoftware/powershell-universal/issues/5312)
  * FilesystemWater is not picking up changes when in vscode mode [#5347](https://github.com/ironmansoftware/powershell-universal/issues/5347)
* Module
  * Stop-PSUJob does not stop external environment jobs [#5318](https://github.com/ironmansoftware/powershell-universal/issues/5318)
  * Grant-PSUAppToken does not return the app token [#5337](https://github.com/ironmansoftware/powershell-universal/issues/5337)
  * Rerun job is missing labels [#5263](https://github.com/ironmansoftware/powershell-universal/issues/5263)
  * New-PSUApp does not restrict creation of apps with relative paths to the repository location [#5333](https://github.com/ironmansoftware/powershell-universal/issues/5333)
* Portal
  * Fixed an issue running scripts from the portal with Windows Authentication
  * Using generated SSH keys from PSU [#5101](https://github.com/ironmansoftware/powershell-universal/issues/5101)
* Platform
  * Run VACUUM in SQLite Groom Job \[#5323]
  * Deployment as Module breaks instance config - file already exists [#5376](https://github.com/ironmansoftware/powershell-universal/issues/5376)
* Tools
  * SQLite to SQL Server migration fails on ComputerTag with IDENTITY\_INSERT OFF [#5320](https://github.com/ironmansoftware/powershell-universal/issues/5320)

## 5.6.9 - 10/22/2025

### Bug Fixes

#### Security

* Updated to latest .NET SDK to address security vulnerabilities

#### Admin Console

* Revoke option for tokens is disabled [#5261](https://github.com/ironmansoftware/powershell-universal/issues/5261)
* Triggering a schedule does not work [#5262](https://github.com/ironmansoftware/powershell-universal/issues/5262)
* Windows Auth users can not execute scripts [#5266](https://github.com/ironmansoftware/powershell-universal/issues/5266)
* Fixed an issue querying jobs when using custom permissions for scripts in folders
* Create App from Command parameter order is important [#5197](https://github.com/ironmansoftware/powershell-universal/issues/5197)
* Script folders are now sorted alphabetically

#### APIs

* Case sensitivity when calling endpoints with Windows Auth and PostgreSQL [#5289](https://github.com/ironmansoftware/powershell-universal/issues/5289)
* Endpoint Test History is not scoped to a specific endpoint [#5299](https://github.com/ironmansoftware/powershell-universal/issues/5299)
* Endpoint Documentation Not Working for Commands and Classes in Modules [#5322](https://github.com/ironmansoftware/powershell-universal/issues/5322)

#### Apps

* Title flicker when using LoadTitle [#5270](https://github.com/ironmansoftware/powershell-universal/issues/5270)
* UDScript/UDPage not found [#5071](https://github.com/ironmansoftware/powershell-universal/issues/5071)
* If Page Name Doesn't Match File, Page Doesn't Load [#5269](https://github.com/ironmansoftware/powershell-universal/issues/5269)
* Saving changes to app in Files tab takes a long time for refresh [#5273](https://github.com/ironmansoftware/powershell-universal/issues/5273)
* Duplicate trigger names causes trigger page to fail to load [#5290](https://github.com/ironmansoftware/powershell-universal/issues/5290)
* Transfer List: New-UDTransferListItem -Disabled not respected [#5300](https://github.com/ironmansoftware/powershell-universal/issues/5300)

#### Automation

* Fixed an issue running scripts with Triggers in nested folders
* Improved performance of progress reporting that was causing SQLite locking issues
* Job Trigger at ServerStartup delay [#5297](https://github.com/ironmansoftware/powershell-universal/issues/5297)

#### Platform

* Deployment module isn't installed as a module [#4901](https://github.com/ironmansoftware/powershell-universal/issues/4901)
* Fixed an issue with child process reporting
* Fixed an issue with account-based licensing installed with environment variables

## 5.6.8 - 9/26/2025

### Bug Fixes

#### Admin Console

* v5 Permissions/Roles [#4954](https://github.com/ironmansoftware/powershell-universal/issues/4954)
* Empty computer groups computer list never loads [#5220](https://github.com/ironmansoftware/powershell-universal/issues/5220)
* Very hard to select reload configuration file(s) [#5242](https://github.com/ironmansoftware/powershell-universal/issues/5242)
* Custom Admin console title is not visible in light mode [#5243](https://github.com/ironmansoftware/powershell-universal/issues/5243)
* The Send to Support button is inoperable [#5232](https://github.com/ironmansoftware/powershell-universal/issues/5232)
* Sending logs to support should include the case number [#5231](https://github.com/ironmansoftware/powershell-universal/issues/5231)
* Looks like the different streams are not coloring correctly in the log [#5033](https://github.com/ironmansoftware/powershell-universal/issues/5033)

#### Agent

* Agent stops creating logs [#4921](https://github.com/ironmansoftware/powershell-universal/issues/4921)
* Published a Linux Docker image for the agent

#### Apps

* Not very intuitive error line numbers in app log [#5219](https://github.com/ironmansoftware/powershell-universal/issues/5219)
* \[5.6.6] ImportExcel module errors but nothing is in the logs [#5202](https://github.com/ironmansoftware/powershell-universal/issues/5202)
* Set-UDClipboard adds an unexpected background color [#5212](https://github.com/ironmansoftware/powershell-universal/issues/5212)
* Developer License tagline moves [#5227](https://github.com/ironmansoftware/powershell-universal/issues/5227)
* For New-UDTable add the 'Search' Box the -InitialState hashtable [#5196](https://github.com/ironmansoftware/powershell-universal/issues/5196)
* New-UDPage Role parameter is reset on save with PSU VSCode Extension [#5236](https://github.com/ironmansoftware/powershell-universal/issues/5236)
* Windows Authentication users getting blank app pages [#5250](https://github.com/ironmansoftware/powershell-universal/issues/5250)

#### APIs

* API Swagger Documentation page throwing error [#5234](https://github.com/ironmansoftware/powershell-universal/issues/5234)
* Endpoint testing returns 401 ClientError when testing from GUI with Authentication Enabled [#5238](https://github.com/ironmansoftware/powershell-universal/issues/5238)

#### Automation

* Pester / Tests page not showing any scripts that end in .Test.ps1 [#5228](https://github.com/ironmansoftware/powershell-universal/issues/5228)
* DBUpdateConcurrencyException in job logs [#5237](https://github.com/ironmansoftware/powershell-universal/issues/5237)

#### Module

* Added Set-PSUSchedule

#### Portal

* Error on resubmission of portal form [#5223](https://github.com/ironmansoftware/powershell-universal/issues/5223)
* Added Jwt\_\_EvaluateClaims to allow for custom claim evaluation in JWT authentication.

#### Platform

* SSH Key error when using git on Linux [#5222](https://github.com/ironmansoftware/powershell-universal/issues/5222)
* \[5.6.6] Scripts not updating when in VS Code mode [#5208](https://github.com/ironmansoftware/powershell-universal/issues/5208)
* Fixed an issue processing PSModulePath in some environments.
* Fixed an issue applying deployments.

## 5.6.7 - 9/11/2025

### Bug Fixes

#### Admin Console

* Vscode / Web toggle bar - always show [#5193](https://github.com/ironmansoftware/powershell-universal/issues/5193)
* Job output log doesn't have word wrap and the show streams/timestamps are not persistent on page refresh [#5025](https://github.com/ironmansoftware/powershell-universal/issues/5025)
* The current user is not the owner error [#5194](https://github.com/ironmansoftware/powershell-universal/issues/5194)
* Install modules to global scope [#4970](https://github.com/ironmansoftware/powershell-universal/issues/4970)
* Branch Switching Issues [#5163](https://github.com/ironmansoftware/powershell-universal/issues/5163)
* Waiting for feedback prompt causes an error on Enter [#5214](https://github.com/ironmansoftware/powershell-universal/issues/5214)
* Selecting all in Git to commit is displaying wrong number of files selected when using "Select All" - 5.5.5 [#5000](https://github.com/ironmansoftware/powershell-universal/issues/5000)
* In endpoints, Roles column bleeds under Tags column [#5207](https://github.com/ironmansoftware/powershell-universal/issues/5207)

#### APIs

* User with apis.endpoints/read access cannot view the endpoints from the ui [#5201](https://github.com/ironmansoftware/powershell-universal/issues/5201)

#### Apps

* Restart App after adding -AutoInclude causes page not found [#5177](https://github.com/ironmansoftware/powershell-universal/issues/5177)
* onClick attribute fails for li tag [#5185](https://github.com/ironmansoftware/powershell-universal/issues/5185)

#### Automation

* Fixed long delays when starting jobs with automatic transcripts enabled
* Fixed an issue with job load balancer randomization causing jobs to concentrate on a single node in a multi-node environment
* $ENV:Temp points to incorrect location when running as another user [#5200](https://github.com/ironmansoftware/powershell-universal/issues/5200)
* Unexpected behavior from variables when used in script documentation [#5210](https://github.com/ironmansoftware/powershell-universal/issues/5210)
* 'Job Completed with Errors' event triggers fires on completed with success [#5209](https://github.com/ironmansoftware/powershell-universal/issues/5209)

#### Module

* Improve Efficiency of Cache Cmdlets [#5095](https://github.com/ironmansoftware/powershell-universal/issues/5095)

#### Platform

* Single letter published folder breaks all apps [#4877](https://github.com/ironmansoftware/powershell-universal/issues/4877)
* Expose if a server is in maintenance mode [#5206](https://github.com/ironmansoftware/powershell-universal/issues/5206)
* Variables defined in Modules//\_universal/variables.ps1 are visible in “Platform - Variables” but aren’t available in runspaces (Get-Variable / module code can’t read them) [#5211](https://github.com/ironmansoftware/powershell-universal/issues/5211)
* Fixed an issue cloning git repositories using SSH keys

## 5.6.6 - 9/2/2025

### Bug Fixes

#### Admin Console

* Date format settings not respected [#5141](https://github.com/ironmansoftware/powershell-universal/issues/5141)
* Improved performance of rendering timestamps
* Move Web/VSCode Toggle up to global bar [#5179](https://github.com/ironmansoftware/powershell-universal/issues/5179)
* Reload All is hidden [#5181](https://github.com/ironmansoftware/powershell-universal/issues/5181)
* Modules from Gallery is not working after 5.6.5 update [#5190](https://github.com/ironmansoftware/powershell-universal/issues/5190)

#### Apps

* Reset-UDTheme Broke [#5136](https://github.com/ironmansoftware/powershell-universal/issues/5136)
* Style Theme Color Help Addition [#5137](https://github.com/ironmansoftware/powershell-universal/issues/5137)
* Invoke-UDRedirect prevents "Open in new tab" from working correctly [#5067](https://github.com/ironmansoftware/powershell-universal/issues/5067)
* Missing useful debug information [#5105](https://github.com/ironmansoftware/powershell-universal/issues/5105)
* Windows Auth: Direct navigation to page with -Role shows “Page Not Found” / $Roles empty until visiting /login (PSU 5.6.4 on IIS) [#5162](https://github.com/ironmansoftware/powershell-universal/issues/5162)
* "Error rendering Dashboard": Please, keep displaying and log this exception! [#5180](https://github.com/ironmansoftware/powershell-universal/issues/5180)

#### Automation

* Improved database performance when starting jobs
* Enable variables for script documentation [#5158](https://github.com/ironmansoftware/powershell-universal/issues/5158)

#### Module

* Fixed a permission issue with Get-PSUScript

#### Platform

* \[5.6.5] another admin site not working after upgrade \[#5169]
* Changing an environment name doesn't update settings [#5150](https://github.com/ironmansoftware/powershell-universal/issues/5150)
* Specify module version for environments. [#5148](https://github.com/ironmansoftware/powershell-universal/issues/5148)
* Module discovery doesn't find modules that don't have a manifest [#5147](https://github.com/ironmansoftware/powershell-universal/issues/5147)
* Module created via Modules page does not appear in list until PSU service is restarted [#4906](https://github.com/ironmansoftware/powershell-universal/issues/4906)
* Upgraded PSResourceGet to 1.1.1
* Persist and display “Last Applied Commit SHA” per node on Git Status (do not clear on no-change sync) [#5188](https://github.com/ironmansoftware/powershell-universal/issues/5188)

#### Portal

* Portal pages require portal.pages/update for widgets to render (read-only roles see blank page) [#5173](https://github.com/ironmansoftware/powershell-universal/issues/5173)

## 5.6.5 - 8/25/2025

### Bug Fixes

#### Admin Console

* Show computers under computer group [#5152](https://github.com/ironmansoftware/powershell-universal/issues/5152)
* Secret variables cannot be selected from the Environments page [#5126](https://github.com/ironmansoftware/powershell-universal/issues/5126)
* Can't set time on schedule [#5112](https://github.com/ironmansoftware/powershell-universal/issues/5112), [#4938](https://github.com/ironmansoftware/powershell-universal/issues/4938), [#4870](https://github.com/ironmansoftware/powershell-universal/issues/4938) Restart app is hard to click [#5165](https://github.com/ironmansoftware/powershell-universal/issues/5165)

#### APIs

* Configurable API process startup timeout for API environments (e.g., Windows PowerShell 5.1 under IIS) [#5161](https://github.com/ironmansoftware/powershell-universal/issues/5161)

#### Apps

* Half of the apps were in a 'stopped' status [#5123](https://github.com/ironmansoftware/powershell-universal/issues/5123)
* Date Range Picker Broken [#5117](https://github.com/ironmansoftware/powershell-universal/issues/5117)
* Apps from Module parameter error [#4822](https://github.com/ironmansoftware/powershell-universal/issues/4822)
* UDRadio: Set-UDElement -Properties @{ Disabled = $true } does not disable the at runtime (4.5.3 and 5.6.4) [#5144](https://github.com/ironmansoftware/powershell-universal/issues/5144)
* Table 'SelectAll' Server-side issues [#4916](https://github.com/ironmansoftware/powershell-universal/issues/4916), [#4931](https://github.com/ironmansoftware/powershell-universal/issues/4931)
* add a new variant to New-UDDivider [#5131](https://github.com/ironmansoftware/powershell-universal/issues/5131)

#### Automation

* Jobs are still getting stuck in queued state when service starts and job executes via trigger [#5116](https://github.com/ironmansoftware/powershell-universal/issues/5116)
* OutOfMemory Exception with Windows PowerShell 5.1 Jobs [#5135](https://github.com/ironmansoftware/powershell-universal/issues/5135) More information about schedules on scripts [#5139](https://github.com/ironmansoftware/powershell-universal/issues/5139)
* Event Handler - Error [#5092](https://github.com/ironmansoftware/powershell-universal/issues/5092)
* Script base path is not honored in custom environment jobs [#5107](https://github.com/ironmansoftware/powershell-universal/issues/5107)
* Some trigger events give additional unexpected arguments [#5159](https://github.com/ironmansoftware/powershell-universal/issues/5159)

#### Module

* Fixed an issue with Get-PSUJob returning child jobs when using -Id or -RunId
* Get-PSUJob doesn't return archived jobs [#5134](https://github.com/ironmansoftware/powershell-universal/issues/5134)
* Get-PSUJob does not return ParentJobId [#4799](https://github.com/ironmansoftware/powershell-universal/issues/4799)
* Invoke-PSUEndpoint returns $null if there are query parameters [#5121](https://github.com/ironmansoftware/powershell-universal/issues/5121)

#### Platform

* \[ERR]\[UniversalAutomation.StartupService] Failed to add license from environment variable. [#5130](https://github.com/ironmansoftware/powershell-universal/issues/5130)
* All ntSecurityDescriptor are empty value - Powershell 7 integrated environment (or external PowerShell 7) [#5111](https://github.com/ironmansoftware/powershell-universal/issues/5111-)
* 4.x / 5.x Modules resources vanish when reloading configs [#4856](https://github.com/ironmansoftware/powershell-universal/issues/4856)
* SessionTimeout set to 0 in settings.ps1 [#5143](https://github.com/ironmansoftware/powershell-universal/issues/5143)
* PSU Fails to start if security environment is missing [#5151](https://github.com/ironmansoftware/powershell-universal/issues/5151)
* scripts.ps1: Production system creates missing files that are empty [#5127](https://github.com/ironmansoftware/powershell-universal/issues/5127)
* Restart of PSU Service "touched" all script files [#5053](https://github.com/ironmansoftware/powershell-universal/issues/5053)
* Force git sync for all machines [#5149](https://github.com/ironmansoftware/powershell-universal/issues/5149)

## 5.6.4 - 8/13/2025

### Bug Fixes

* Fixed an issue with New-UDButton
* Fixed an issue viewing job output

## 5.6.3 - 8/12/2025

### Bug Fixes

#### Admin Console

* Admin Console JavaScript Errors [#5096](https://github.com/ironmansoftware/powershell-universal/issues/5096)
* Clear Cache from /admin/platform/cache [#5080](https://github.com/ironmansoftware/powershell-universal/issues/5080)
* End time filtering not working [#5006](https://github.com/ironmansoftware/powershell-universal/issues/5006)
* Issue with editing variables in the UI in web view mode. [#5034](https://github.com/ironmansoftware/powershell-universal/issues/5034)
* Optimized Automation \ Schedules page [#5104](https://github.com/ironmansoftware/powershell-universal/issues/5104)

#### Apps

* cross threaded console logs [#5049](https://github.com/ironmansoftware/powershell-universal/issues/5049)
* New-UDCheckbox LabelPlacement value is case-sensitive (and other properties as well) [#5010](https://github.com/ironmansoftware/powershell-universal/issues/5010)
* Slide transitions are not working [#3460](https://github.com/ironmansoftware/powershell-universal/issues/3460)

#### Automation

* Jobs get stuck when cancelling [#5078](https://github.com/ironmansoftware/powershell-universal/issues/5078)

#### Cmdlets

* Set-PSUCache does not store nested objects well after 3 depth [#5086](https://github.com/ironmansoftware/powershell-universal/issues/5086)

## 5.6.2 - 8/5/2025

### Bug Fixes

#### Admin Console

* cannot click on menu items in /admin [#5013](https://github.com/ironmansoftware/powershell-universal/issues/5013)
* Intelisense no working right [#5019](https://github.com/ironmansoftware/powershell-universal/issues/5019)
* Password Expiration Days and Password Length settings linked [#5037](https://github.com/ironmansoftware/powershell-universal/issues/5037)
* \[5.6.0] Modules tab gets out of sync from the files tab [#5021](https://github.com/ironmansoftware/powershell-universal/issues/5021)
* \[5.6.0] Help refresh kills editor focus [#5018](https://github.com/ironmansoftware/powershell-universal/issues/5018)
* View Page goes to a bad url [#4912](https://github.com/ironmansoftware/powershell-universal/issues/4912)
* Logout goes to a 401 [#5059](https://github.com/ironmansoftware/powershell-universal/issues/5059)
* Fixed admin console cache breaking issue
* Testing an API endpoint causes a service crash [#4972](https://github.com/ironmansoftware/powershell-universal/issues/4972)
* Invalid Average Execution Time [#5061](https://github.com/ironmansoftware/powershell-universal/issues/5061)
* Ctrl+S Allows Save When Save Icon is Disabled [#5063](https://github.com/ironmansoftware/powershell-universal/issues/5063)
* Saving changes to a script in the web UI often spins and doesn't receive the completed response [#5017](https://github.com/ironmansoftware/powershell-universal/issues/5017)
* unable to delete identity when in one-way mode [#5070](https://github.com/ironmansoftware/powershell-universal/issues/5070)
* Fixed permission issues with resources in the admin console

#### Agent

* Fixed an issue with the agent service and scripts that were not fully qualified paths

#### Apps

* Fixed an issue where pages would be added twice
* \[5.5.2] Missing Restart Dashboard and Admin Console from app [#4747](https://github.com/ironmansoftware/powershell-universal/issues/4747)

#### API

* Rate Limit not being honored [#5051](https://github.com/ironmansoftware/powershell-universal/issues/5051)
* Cannot access password from C# API Credential Secrets [#5057](https://github.com/ironmansoftware/powershell-universal/issues/5057)

#### Automation

* Pester / Tests page not showing any scripts that end in Test [#5039](https://github.com/ironmansoftware/powershell-universal/issues/5039)
* Since 5.6.1, jobs are not being logged with their tags [#5056](https://github.com/ironmansoftware/powershell-universal/issues/5056)
* Using a non-existent computer for Default Run As prevents jobs from running [#5062](https://github.com/ironmansoftware/powershell-universal/issues/5062)
* Script with parameter \[FILE] doesn't work anymore [#5076](https://github.com/ironmansoftware/powershell-universal/issues/5076)
* RunAs jobs use service-account TEMP directory instead of impersonated userâ€™s TEMP in PSU 5.5.x [#5075](https://github.com/ironmansoftware/powershell-universal/issues/5075)
* Groom Job never delete old jobs [#5058](https://github.com/ironmansoftware/powershell-universal/issues/5058)

#### Platform

* Set git repository owner [#4569](https://github.com/ironmansoftware/powershell-universal/issues/4569)
* Cannot access a disposed object. Object name: 'System.IO.FileSystemWatcher'. [#5041](https://github.com/ironmansoftware/powershell-universal/issues/5041)
* BaGetter repository does not work in PSU [#4971](https://github.com/ironmansoftware/powershell-universal/issues/4971)
* Updated to Microsoft.PowerShell.SDK 7.5.2

## 5.6.1 - 7/25/2025

### Bug Fixes

#### CVE

* \[CVE-2025-54552] - Apps Docs > Variables includes database connection string with plain text password [#5026](https://github.com/ironmansoftware/powershell-universal/issues/5026)

#### Admin Console

* Jobs \ Computer column not populated in 5.5.5 [#4996](https://github.com/ironmansoftware/powershell-universal/issues/4996)
* Import script does not allow searching. [#5009](https://github.com/ironmansoftware/powershell-universal/issues/5009)

#### Automation

* Invoke-PSUScript from App taking a very long time to trigger [#4238](https://github.com/ironmansoftware/powershell-universal/issues/4238)

#### Apps

* Problems with UDTextbox [#5004](https://github.com/ironmansoftware/powershell-universal/issues/5004)
* Icon and Title missing space in New-UDPages [#4963](https://github.com/ironmansoftware/powershell-universal/issues/4963)

#### Installer

* MSI v5 installer should detect if PSU v4 is running and fail with a warning [#5005](https://github.com/ironmansoftware/powershell-universal/issues/5005)

#### Platform

* psudb should identify SQLite databases [#4999](https://github.com/ironmansoftware/powershell-universal/issues/4999)
* 5.5.5 - Overloads postgreSQL database [#4968](https://github.com/ironmansoftware/powershell-universal/issues/4968)
* Configuration error displayed in UI and error in log as well. [#5016](https://github.com/ironmansoftware/powershell-universal/issues/5016)

## 5.6.0 - 7/22/2025

### Features

#### Admin Console

* Login Page Styling Improvements [#4698](https://github.com/ironmansoftware/powershell-universal/issues/4698)
* Allow separate Dark/Light modes for the Code Editor [#4690](https://github.com/ironmansoftware/powershell-universal/issues/4690)
* Add last execution date/time for schedules page [#4584](https://github.com/ironmansoftware/powershell-universal/issues/4584)
* Notifications 99+ in red [#4758](https://github.com/ironmansoftware/powershell-universal/issues/4758)
* Install module from PSGallery with specific version [#4775](https://github.com/ironmansoftware/powershell-universal/issues/4775)
* show logging icon for an app in module [#4712](https://github.com/ironmansoftware/powershell-universal/issues/4712)
* Show line numbers and minimap by default [#4717](https://github.com/ironmansoftware/powershell-universal/issues/4717)
* Add Splitter Panels in Admin Console [#4797](https://github.com/ironmansoftware/powershell-universal/issues/4797)
* View files in published folders [#4638](https://github.com/ironmansoftware/powershell-universal/issues/4638)
* Improve validation of Endpoint URL [#3789](https://github.com/ironmansoftware/powershell-universal/issues/3789)
* Switch to editor after creating script [#4861](https://github.com/ironmansoftware/powershell-universal/issues/4861)
* Admin Console Idle Timeout [#4585](https://github.com/ironmansoftware/powershell-universal/issues/4585)

#### Agent

* Track agent scripts and reload service if changed [#4674](https://github.com/ironmansoftware/powershell-universal/issues/4674)
* Admin console sessions list should show IPv4 and IPv6 in separate columns [#4606](https://github.com/ironmansoftware/powershell-universal/issues/4606)
* Add Description to agent.json [#4829](https://github.com/ironmansoftware/powershell-universal/issues/4829)

#### APIs

* Configure Swagger Default Documents [#4716](https://github.com/ironmansoftware/powershell-universal/issues/4716)

#### Apps

* New-UDRow Styling [#4783](https://github.com/ironmansoftware/powershell-universal/issues/4783)
* Load data when expand for expansion on UDCard? [#3761](https://github.com/ironmansoftware/powershell-universal/issues/3761)
* Support for groupings within the AutoComplete component [#4779](https://github.com/ironmansoftware/powershell-universal/issues/4779)
* Expose ID property in $Eventdata variable [#4623](https://github.com/ironmansoftware/powershell-universal/issues/4623)
* Add Excel Filter Pattern to select more than on filter to New-UDTableColumn -FilterType [#4694](https://github.com/ironmansoftware/powershell-universal/issues/4694)
* Added Reset-UDTheme
* App Page Editor doesn't show outer 'New-UDPage' cmdlet [#4021](https://github.com/ironmansoftware/powershell-universal/issues/4021)
* Auto-Add Option for App Pages [#4736](https://github.com/ironmansoftware/powershell-universal/issues/4736)
* Prevent Accidental App Restarts When Accessing "View/Edit Code" [#4913](https://github.com/ironmansoftware/powershell-universal/issues/4913)

#### Automation

* Added upload script button
* Discover scripts button [#4212](https://github.com/ironmansoftware/powershell-universal/issues/4212)
* Schedules: Allow folders for organization [#3268](https://github.com/ironmansoftware/powershell-universal/issues/3268)
* Increase Invisibility Timeout to 7 days [#4990](https://github.com/ironmansoftware/powershell-universal/issues/4990)

#### Module

* Added -Detail to Get-PSUCache [#4589](https://github.com/ironmansoftware/powershell-universal/issues/4589)
* Test-PSUAppToken [#4573](https://github.com/ironmansoftware/powershell-universal/issues/4573)

#### Platform

* Added Name to runspace information
* Declarative Settings and Resources for PSU [#4787](https://github.com/ironmansoftware/powershell-universal/issues/4787)
* Environment Recycling [#4703](https://github.com/ironmansoftware/powershell-universal/issues/4703)
* Disable Database Vault [#4536](https://github.com/ironmansoftware/powershell-universal/issues/4536)
* \[5.5.2] Missing Branch [#4750](https://github.com/ironmansoftware/powershell-universal/issues/4750)
* Support for Managing GitHub Deploy Keys in PowerShell Universal (PSU) [#3488](https://github.com/ironmansoftware/powershell-universal/issues/3488)
* Admin account will not allow login after 3 months with no indication except "bad username or password" [#4595](https://github.com/ironmansoftware/powershell-universal/issues/4595)
* Improve Notifications View [#4874](https://github.com/ironmansoftware/powershell-universal/issues/4874)
* Improve Status API [#4869](https://github.com/ironmansoftware/powershell-universal/issues/4869)
* Docker arm container image is not arm [#4903](https://github.com/ironmansoftware/powershell-universal/issues/4903)
* Add NodeName to configuration file runspace [#4973](https://github.com/ironmansoftware/powershell-universal/issues/4973)

### Bugs

#### Admin Console

* \[5.5.3] Excessive Runspace Usage in Integrated Environment [#4741](https://github.com/ironmansoftware/powershell-universal/issues/4741)
* Error when viewing changes before commit [#4766](https://github.com/ironmansoftware/powershell-universal/issues/4766)
* Merge Conflict Wizard Allows Commit with Unresolved Conflict Markers, Corrupting Pages [#4815](https://github.com/ironmansoftware/powershell-universal/issues/4815)
* \[5.5.2] Unable to reload initialize.ps1 [#4731](https://github.com/ironmansoftware/powershell-universal/issues/4731)
* \[5.4.4] System.ObjectDisposedException in JobPage.razor causes persistent job state access errors and UI instability [#4760](https://github.com/ironmansoftware/powershell-universal/issues/4760)
* Unreliable IntelliSense, double scrollbar and missing fullscreen in v5.5.2 GUI [#4814](https://github.com/ironmansoftware/powershell-universal/issues/4814)
* script filter box too narrow [#4834](https://github.com/ironmansoftware/powershell-universal/issues/4834)
* \[5.5.2] first run license import fail [#4727](https://github.com/ironmansoftware/powershell-universal/issues/4727)
* intelisense deletes the first char [#4917](https://github.com/ironmansoftware/powershell-universal/issues/4917)
* Forms authentication loses returnUrl after failed login in PSU 5.5.1 [#4935](https://github.com/ironmansoftware/powershell-universal/issues/4935)
* Unauthorized redirect does not display custom branding when user lacks dashboard role [#4810](https://github.com/ironmansoftware/powershell-universal/issues/4810)
* \[5.6] Schedule last run reports incorrect time [#4929](https://github.com/ironmansoftware/powershell-universal/issues/4929)
* \[5.5.2] Repository doesn't point at a valid Git repository or workdir. [#4729](https://github.com/ironmansoftware/powershell-universal/issues/4729)
* Discarding changes doesn't update count [#4886](https://github.com/ironmansoftware/powershell-universal/issues/4886)
* Severe UI slowdown when notifications table grows to \~150 000 entries while log level is set to Information [#4959](https://github.com/ironmansoftware/powershell-universal/issues/4959)
* Editor issues in v5 (5.6) [#4983](https://github.com/ironmansoftware/powershell-universal/issues/4983)
* Permissions can be created but not deleted in RO mode [#4976](https://github.com/ironmansoftware/powershell-universal/issues/4976)
* Unable to save Verbose preference in Settings/General [#4977](https://github.com/ironmansoftware/powershell-universal/issues/4977)

#### APIs

* Enhance Documentation for accessing secrets for C# API Credential (Issue #4681) [#4817](https://github.com/ironmansoftware/powershell-universal/issues/4817)
* Agent output streams not redirected to job log [#4803](https://github.com/ironmansoftware/powershell-universal/issues/4803)

#### Apps

* \[5.5.0] Windows Auth - identity missmatch [#4663](https://github.com/ironmansoftware/powershell-universal/issues/4663)
* New-UDTextbox: icon is ignored when used in combination with -maskpattern [#4839](https://github.com/ironmansoftware/powershell-universal/issues/4839)
* UDDataGrid Error on No Data [#4767](https://github.com/ironmansoftware/powershell-universal/issues/4767)
* \[5.5.2] Write-PSULog doesn't write to logs within Apps [#4855](https://github.com/ironmansoftware/powershell-universal/issues/4855)
* Missing New-UDDivider in docs #4905
* New-UDExpansionPanel Icon is smashed and it needs a space [#4928](https://github.com/ironmansoftware/powershell-universal/issues/4928)
* UDSelect not aligned vertically when Value is set [#4518](https://github.com/ironmansoftware/powershell-universal/issues/4518)
* New-UDRadioGroup label color is incorrect (disappears) in dark mode when a radio is selected in the group. [#3215](https://github.com/ironmansoftware/powershell-universal/issues/3215)
* Child dashboard pages under /dashboards/SelfService/Pages no longer auto-reload after save in VS Code [#4884](https://github.com/ironmansoftware/powershell-universal/issues/4884)
* OnEnter (UDButton) has stopped working after upgrading to v5 [#4864](https://github.com/ironmansoftware/powershell-universal/issues/4864)
* \[5.5.4] Slow UDAutocomplete #[4846](https://github.com/ironmansoftware/powershell-universal/issues/4846)
* Apps view/read allows users to start/stop/restart all apps [#4986](https://github.com/ironmansoftware/powershell-universal/issues/4986)

#### Automation

* Script gets deleted if there is an error when moving script [#4765](https://github.com/ironmansoftware/powershell-universal/issues/4765)
* \[5.5.2] Job log results don't expand to fill space [#4744](https://github.com/ironmansoftware/powershell-universal/issues/4744)
* Write-Host -NoNewLine not working correctly in PSU Scripts. [#4840](https://github.com/ironmansoftware/powershell-universal/issues/4840)
* Retry job running on node that's not part of original scheduled computer group [#4813](https://github.com/ironmansoftware/powershell-universal/issues/4813)
* \[5.5.3] Scripts from modules don't show in folder view [#4843](https://github.com/ironmansoftware/powershell-universal/issues/4843)
* \[5.5.0] Issue with DateOnly and TimeOnly parameters [#4684](https://github.com/ironmansoftware/powershell-universal/issues/4684)
* Script Documentation / Markdown view [#4922](https://github.com/ironmansoftware/powershell-universal/issues/4922)
* Jobs stuck in queued state [#4989](https://github.com/ironmansoftware/powershell-universal/issues/4989)

#### Diagnostics

* \[5.5.2] Health Check Failed: Missing Environment [#4743](https://github.com/ironmansoftware/powershell-universal/issues/4743)

#### Module

* SecureString visible in job parameters when script is called using Invoke-PSUScript [#4784](https://github.com/ironmansoftware/powershell-universal/issues/4784)
* Grant-PSUAppToken response shows 0 for ID [#4902](https://github.com/ironmansoftware/powershell-universal/issues/4902)

#### Platform

* Cached values dont observe expiration rules once the value is read [#4798](https://github.com/ironmansoftware/powershell-universal/issues/4589)
* \[5.6.0] Git commit preview (manual mode) shows last 2 changes [#4816](https://github.com/ironmansoftware/powershell-universal/issues/4816)
* Documentation for configuring VS Code Extension from PSU Admin is out of date [#4853](https://github.com/ironmansoftware/powershell-universal/issues/4853)
* Universal Server Process reports 0 bytes of memory [#4898](https://github.com/ironmansoftware/powershell-universal/issues/4898)
* Process View Shows Old Processes [#4895](https://github.com/ironmansoftware/powershell-universal/issues/4895)
* psuignore doesn't hide files or folders [#4944](https://github.com/ironmansoftware/powershell-universal/issues/4944)

## 5.5.5 - 7/9/2025

### Bugs

#### Admin Console

* Built in widgets not saved in portal pages [#4909](https://github.com/ironmansoftware/powershell-universal/issues/4909)

#### APIs

* Eventhub sends payload of 'test' when data is sent to a Computer or ConnectionID in 5.5.4 [#4896](https://github.com/ironmansoftware/powershell-universal/issues/4896)

#### Automation

* \[5.5.4] 'Cannot find drive. A drive with the name 'Cert' does not exist.' when using Windows Powershell 5.1 [#4845](https://github.com/ironmansoftware/powershell-universal/issues/4845)
* \[5.5.4] 'The term 'New-Guid' is not recognized as the name of a cmdlet, function, script file, or operable program.' when using Windows Powershell 5.1 [#4844](https://github.com/ironmansoftware/powershell-universal/issues/4844)
* files in all sub folders are shown [#4835](https://github.com/ironmansoftware/powershell-universal/issues/4835)
* Scripts root level folder shows all scripts including nested [#4851](https://github.com/ironmansoftware/powershell-universal/issues/4851)
* \[5.5.4] Script Duplication [#4847](https://github.com/ironmansoftware/powershell-universal/issues/4847)
* Edit Properties Dialog Pagination issue [#4850](https://github.com/ironmansoftware/powershell-universal/issues/4850)
* Scripts with -ConcurrentJobs x parameter defined, stuck in queue [#4862](https://github.com/ironmansoftware/powershell-universal/issues/4862)
* Memory leak in PSU server [#4892](https://github.com/ironmansoftware/powershell-universal/issues/4892)
* Scheduler fails to register server node; jobs stuck with 0001-12-31 StartTime after upgrade to 5.5.4 [#4934](https://github.com/ironmansoftware/powershell-universal/issues/4934)
* Improved performance of Write-Progress

#### Platform

* Creating or deleting a deployment in admin console doesn't refresh deployment list [#4891](https://github.com/ironmansoftware/powershell-universal/issues/4891)
* Run As accounts using local login rather than batch [#4904](https://github.com/ironmansoftware/powershell-universal/issues/4904)

## 5.5.4 - 6/3/2025

### Bugs

#### Admin Console

* Improved IntelliSense and Help performance
* Fixed an issue with the permissions on the module editor page

#### Apps

* \[5.5.0] Invoke-UDJavascript throws exceptions [#4656](https://github.com/ironmansoftware/powershell-universal/issues/4656)
* New-UDGridLayout not working since 5.3.x [#4575](https://github.com/ironmansoftware/powershell-universal/issues/4575)

#### Automation

* Reloading scripts in PSU 5.5.2 causes EF tracking conflict when using ParameterSetName in script definitions [#4751](https://github.com/ironmansoftware/powershell-universal/issues/4751)
* OneTime Schedules Are Not Persisting or Removable Across Restarts in PSU v5.5.3 [#4763](https://github.com/ironmansoftware/powershell-universal/issues/4763)
* Regression – POST /api/v1/script/path/{scriptFullPath} returns “Data at the root level is invalid” and fails to bind parameters in PSU 5.x [#4828](https://github.com/ironmansoftware/powershell-universal/issues/4828)

#### Platform

* Scheduler resets and DB‑lock timeouts in PSU5.5.x Hangfire jobs stop executing, queues refill, or concentrate on one node after upgrade [#4780](https://github.com/ironmansoftware/powershell-universal/issues/4780)
* psu not executable by default on Linux [#4832](https://github.com/ironmansoftware/powershell-universal/issues/4832)
* Fixed an issue where certain docker images were targeting PS 7.3 rather than 7.5.
* RunAs sessions do not inherit PSModulePath, causing built-in module load failures [#4769](https://github.com/ironmansoftware/powershell-universal/issues/4769)
* \[5.3.2] Deployment Error [#4417](https://github.com/ironmansoftware/powershell-universal/issues/4417)
* Added log messages for slow SQL queries
* Long Running Queries [#4841](https://github.com/ironmansoftware/powershell-universal/issues/4841)
* Git sync crashes in 5.5.1 [#4702](https://github.com/ironmansoftware/powershell-universal/issues/4702)

## 5.5.3 - 5/19/2025

### Bugs

#### Admin Console

* \[5.5.2] Error in Logs from EditorService [#4724](https://github.com/ironmansoftware/powershell-universal/issues/4724)
* \[5.5.0] Removing Auth from a Portal Page Doesn't Display Properly [#4683](https://github.com/ironmansoftware/powershell-universal/issues/4683)
* \[5.5.3] Settings not applying ? [#4728](https://github.com/ironmansoftware/powershell-universal/issues/4728)
* \[5.5.2] Cannot see fatal errors [#4733](https://github.com/ironmansoftware/powershell-universal/issues/4733)
* \[5.5.2] View Page in nestedIIS does not work [#4746](https://github.com/ironmansoftware/powershell-universal/issues/4746)
* \[5.5.3] label on "create script" button turns into "View Properties" (x2) [#4734](https://github.com/ironmansoftware/powershell-universal/issues/4734)
* \[5.5.2] Can't create tokens or identities in one-way git sync [#4753](https://github.com/ironmansoftware/powershell-universal/issues/4753)
* \[5.5.2] Git commit list expand/contract button is missing [#4768](https://github.com/ironmansoftware/powershell-universal/issues/4768)
* \[5.5.2] Forced Git Sync can fail if admin console page is reloaded [#4792](https://github.com/ironmansoftware/powershell-universal/issues/4792)
* \[5.5.2] IIS WebSocket health check typo [#4794](https://github.com/ironmansoftware/powershell-universal/issues/4794)
* \[5.5.2] Clear Health Checks button throws an error [#4793](https://github.com/ironmansoftware/powershell-universal/issues/4793)
* Repository modules search [#4773](https://github.com/ironmansoftware/powershell-universal/issues/4773)
* \[5.5.2] Not Authenticated Error with Windows Auth [#4790](https://github.com/ironmansoftware/powershell-universal/issues/4790)

#### APIs

* \[5.5.0] Accessing PSU Variables / Secrets in Csharp Endpoint [#4681](https://github.com/ironmansoftware/powershell-universal/issues/4681)

#### Apps

* Optimize Table Component Refresh Speed (Target: <0.2s) [#4622](https://github.com/ironmansoftware/powershell-universal/issues/4622)
* \[5.5.2] New-UDDateRangePicker shows MUI X expired error [#4776](https://github.com/ironmansoftware/powershell-universal/issues/4776)
* \[5.5.0] Regression: -HeaderFilters no longer enables header filters in DataGrid [#4771](https://github.com/ironmansoftware/powershell-universal/issues/4771)
* \[5.5.2] Hide-UDModal defaults to -All [#4781](https://github.com/ironmansoftware/powershell-universal/issues/4781)
* \[5.5.2] New-UDAutocomplete only shows first item in the list [#4774](https://github.com/ironmansoftware/powershell-universal/issues/4774)
* \[5.5.2] Scripts run from a Dashboard using Invoke-PSUScript now show as Identity=System in Job list. [#4770](https://github.com/ironmansoftware/powershell-universal/issues/4770)

#### Automation

* \[5.5.2] 'Default Run On' setting is being ignored [#4745](https://github.com/ironmansoftware/powershell-universal/issues/4745)

#### Cmdlets

* \[5.5.0] Get-PSUComputer not returning tags [#4718](https://github.com/ironmansoftware/powershell-universal/issues/4718)
* \[5.5.0] Set-PSUCache AbsoluteExpiration does not work with non-US time formats [#4725](https://github.com/ironmansoftware/powershell-universal/issues/4725)
* \[5.5.2] Fix the error message -> Invalid URI: The format of the URI could not be determined. [#4749](https://github.com/ironmansoftware/powershell-universal/issues/4749)

#### Platform

* \[5.5.1] Execution policy for PSU-installed modules [#4720](https://github.com/ironmansoftware/powershell-universal/issues/4720)
* \[5.3.2] Graceful shutdown of PSU Service on Linux takes a long time [#4506](https://github.com/ironmansoftware/powershell-universal/issues/4506)
* \[5.5.2] Locked out after git repository delete [#4788](https://github.com/ironmansoftware/powershell-universal/issues/4788)
* \[5.2.0] Users with no role gain access to role assigned apps [#4315](https://github.com/ironmansoftware/powershell-universal/issues/4315)

#### Security

* \[5.5.2] Error Creating Permissions [#4730](https://github.com/ironmansoftware/powershell-universal/issues/4730)

## 5.5.2 - 4/29/2025

### Bugs

#### Apps

* \[5.5.0] New-UDRow Unable to set ID [#4700](https://github.com/ironmansoftware/powershell-universal/issues/4700)
* \[5.5.1] New-UDTransferList only renders first item when populated dynamically or statically in Windows PowerShell 5.1 [#4625](https://github.com/ironmansoftware/powershell-universal/issues/4625)

#### Admin Console

* Added a warning when adding roles to secret variables
* \[5.5.1] Average Execution Time seems overly precise [#4697](https://github.com/ironmansoftware/powershell-universal/issues/4697)
* \[5.5.1] missing job history for scripts called with Invoke-PSUScript [#4706](https://github.com/ironmansoftware/powershell-universal/issues/4706)

#### Automation

* Fixed an issue changing script base folder

#### Platform

* Improved error messages for GMSA account login failures
* Improved assembly load logging for PowerShell 7 environment.
* \[5.5.0] Git sync not working [#4679](https://github.com/ironmansoftware/powershell-universal/issues/4679)
* \[5.5.0] License file not expiring properly [#4693](https://github.com/ironmansoftware/powershell-universal/issues/4693)
* Fixed an issue when $ENV:PSModulePath was set in the user scope
* \[5.5.0] Git settings persisting despite deletion [#4699](https://github.com/ironmansoftware/powershell-universal/issues/4699)
* Updated to PowerShell SDK 7.5.1 and .NET SDK 9.0.203

#### Portal

* \[5.5.0] Custom Widget Properties Showing Non-Existent Properties [#4667](https://github.com/ironmansoftware/powershell-universal/issues/4667)
* \[5.5.1] Portal - Side bar navigation between scripts only works for the first script select [#4708](https://github.com/ironmansoftware/powershell-universal/issues/4708)

#### VS Code

* \[5.5.1] Script Base Path causes VS Code Extension to fail to load scripts. [#4715](https://github.com/ironmansoftware/powershell-universal/issues/4715)

## 5.5.1 - 4/23/2025

### Bugs

#### Admin Console

* Fixed an issue with the API endpoint tester (#4658)
* Fixed an issue with filtering on a script's job page (#4661)
* Fixed an issue creating and updating endpoints (#4657)
* Fixed an issue validating GMSA credentials in the admin console
* Fixed a crash that could occur when viewing job data (#4659)
* Fixed an issue with tag colors (#4673)
* Fixed an issue with the merge conflict resolution dialog (#4630)
* Fixed an issue display timestamps for jobs

#### Apps

* Fixed an issue with row selection in New-UDTable (#4614)

#### Automation

* Fixed an errant log message in jobs started as another user (#4666)

#### Platform

* Fixed a redirect loop when initiating OpenID Connect logins from the login page
* Fixed an issue where the groom job could become unscheduled (#4664)
* Fixed an issue connecting using the Az.Authentication module
* Fixed an issue listing runspaces and assemblies for the PSU server process

#### Module

* Fixed an issue with Write-PSULog in jobs (#4652)

#### VS Code

* Fixed an issue with the VS Code debugger (#4627)

## 5.5.0 - 4/15/2025

### Features

#### Admin Console

* Event Hub connections are now listed under their respective Event Hub (#4451)
* Excluded scripts are now persistent (#4467)
* Script filter is now multiselect on the jobs page (#4020)
* Added known environment variables to support page (#3578)

#### Automation

* Added Computer Offline trigger (#4461)
* Added global preference variable settings (#3779)
* Added support for script permissions (#3941)

#### Apps

* Added -Critical to New-PSUApp (#4118)
* Added New-UDGauge (#4455)
* Added -MaskPattern to New-UDTextbox (#4236)
* Added -Indeterminate to New-UDCheckbox (#4424)
* Added -MountOnEnter and -UnmountOnExit to New-UDTransition (#4449)
* Added -All to Hide-UDModal (#4557)
* Added MUI Sparklines support to New-UDSparkline (#4489)
* Added -Attributes to New-UDTextbox (#4048)
* Added more examples to New-UDAvatar to match MUI documentation (#2170)

#### APIs

* C# endpoints now support references and using statements
* Event Hub Connections now return agent version (#4553)

#### Module

* Added Measure-PSUConvertToJsonDepth (#4309)
* Added -Limit to Get-PSUJobOutput (#4516)
* Added Get-PSUEventHub (#4525)
* Added -AsObject to Get-PSUJobOutput (#4496)
* Added -Scope and -Credential to Connect-PSUServer
* Added Disconnect-PSUServer

#### Platform

* Added support for powershell.exe environments
* Added support for app tokens with multiple roles (#4479)
* Added horizontal login page layout (#4147)
* Added support for Windows Form Login (#4521)

### Bug Fixes

#### Admin Console

* Fixed an issue updating git repository settings (#4524)
* Fixed an issue with the git diff editor theme color (#4530)
* Fixed an issue viewing portal resources (#4546)
* Fixed an issue deleting non-empty folders (#4549)
* Fixed an issue archiving jobs with child jobs (#4545)
* Fixed an issue creating a script in a deeply nested folder (#4605)

#### Agent

* Fixed an issue returning domain name of agent (#4554)

#### Apps

* Fixed an issue with page icons (#4466)
* Fixed an issue with New-UDNivoChart -Heatmap (#4528)
* Fixed an issue with UDStepper buttons (#4444)
* Fixed an issue displaying tables with no data (#4561)
* Fixed an issue with finally blocks not being called when sessions expired (#4448)
* Fixed an issue loading apps with ErrorActionPreference set to stop (#4564)
* Fixed an issue with New-UDTextbox, New-UDForm and Set-UDElement (#4202)
* Fixed an encoding issue with exporting CSVs from New-UDTable (#2094)
* Fixed an issue with New-UDTransferList search (#4294)
* Fixed an issue with New-UDTreeView (#4613)

#### APIs

* Fixed an issue reloading API endpoints from disk in nested paths (#4458)
* Fixed an issue updating an endpoint path if the file already exists (#4635)

#### Automation

* Fixed an issue with manually running a script against a computer group with nodes in maintenance mode (#4400)
* Fixed an issue with re-queued continuous and one-time jobs (#4522)
* Fixed an issue calling exit with non-zero exit codes in scripts (#4492)
* Fixed an issue updating a script that had a parameter in multiple parameter sets (#4532)
* Fixed an issue uploading files to a script (#4602)

#### Cmdlets

* Fixed an issue with mixed slashes and Invoke-PSUScript (#4578)
* Fixed an issue with Set-PSUCache (#4604)
* Fixed an issue with Set-PSUVariable (#4590)
* Fixed issues with Invoke-PSUScript -WaitTimeout (#4611, #4610)
* Fixed an issue with Invoke-PSUScript output repeating (#4491)

#### Diagnostics

* Fixed an issue with the Missing Environment health check (#4470)

#### Platform

* Fixed an issue detecting updated PowerShell versions (#4398)
* Fixed an issue with password reset and expiration (#4464)
* Fixed a display issue with modules in the admin console (#4507)
* Fixed an issue with data retention days set below 30 (#4519)
* Removed support for Application Insights instrumentation key (No longer supported by Microsoft)
* Fixed an issue with git edit mode (#4538)
* Fixed an issue with Windows PowerShell 5.1 PSModulePath (#4542)
* Fixed an issue with roles provided by modules (#4547)
* Fixed an issue with MicrosoftTeams and Az.Accounts module (#4581)
* Fixed an issue with WS-Federation in appsettings.json (#4579)
* Fixed an issue with ExchangeOnlineManagement module (#4592)

## 5.4.4 - 4/2/2025

### Bug Fixes

#### Automation

* Fixed an issue running jobs as Group Managed Service Accounts (#4548)

#### APIs

* Fixed an issue updating endpoints with nested paths from outside the admin console

#### Security

* Fixed an issue saving roles (#4574)
* Disabled Pushed Authorization Requests for OpenID Connect (#4586)

#### Platform

* Fixed an issue with Microsoft.Graph, Az.Accounts, and MicrosoftTeams modules (#4581)

## 5.4.3 - 3/23/2025

### Bug Fixes

#### Security

* Fixed an issue with role policy scripts not running properly after startup

## 5.4.2 - 3/17/2025

### Bug Fixes

#### Admin Console

* Fixed an issue with the Create Script dialog and folders (#4501)

#### APIs

* Fixed an issue with the default endpoints.json docs (#4504)

#### Apps

* Fixed an issue starting apps that were a part of a computer group (#4493)
* Fixed a UDTable rendering issue (#4495)

#### Module

* Fixed an issue loading the Universal module in PowerShell 7.4.x

#### Platform

* Fixed an execution policy issue with vaults.ps1
* Fixed an errant log message in standard out (#4500)
* Fixed an issue where scripts contents could be overwritten with the default value

## 5.4.1 - 3/13/2025

### Bug Fixes

#### Admin Console

* Fixed a login issue with Windows authentication (#4471)

#### Automation

* Fixed an issue with schedules set to a specific computer

#### Module

* Fixed an issue with -Integrated switch

#### Platform

* Updated .NET SDK to address CVE-2025-24070
* Fixed an issue with expiration of persistent cache items (#4472)
* Fixed an issue updating the database schema with PostgreSQL (#4485)

## 5.4.0 - 3/11/2025

### Features

#### Admin Console

* Add PSU Admin CLI (#4099)
* Added script metrics to script page (#4191)
* Added validate secret button on Windows (#4321)
* Added Create App From Command button (#4383)
* Added Import Windows Roles button (#4218)
* Added Danish language support
* Git commits now display line breaks for messages (#4318)

#### Automation

* Added least busy server load balancer for jobs (#3199)
* Cancelling a parent job now cancels all child jobs (#4336)
* Added View Jobs button to scripts table (#4353)
* Added the option to not delete the script file when removing a script from the admin console (#4320)
* Added support for run as of Group Managed Service Accounts (#2430)

#### Apps

* Added -LoadingComponent to New-UDIconButton (#4340)
* Added -Version to New-UDGrid (#2159)
* Added -ExportOptions to New-UDDataGrid
* Added search to built in docs (#3042)

#### APIs

* Added history to the API tester (#4097)
* Added -Timeout to Send-PSUEvent (#4354)
* Added EventHubConnect and EventHubDisconnect to trigger types (#4394)
* Added -Disabled to New-PSUEndpoint (#4407)
* Added OpenAPI Example support (#4184)

#### Git

* Added Create Branch button (#4334, #3075)

#### Platform

* Updated to PowerShell 7.5.0 and .NET 9.0
* Added .psuignore (#4195)
* File system logging now defaults to specific log file folders (#4346)
* Added Blocked File health check (#2609)
* Added -Type parameter to Environments
* Added Blank Item Templates (#4312)
* Renamed agent logs to host.txt for PowerShell host processes (#4392)
* Added -DisableFirstRun to Set-PSUSettings (#4399)
* Added secret support to configuration files (#4397)
* Groom job now cleans event hub connections (#4410)
* Added PSScriptAnalyzer module to installation media
* Debugger Environment is no longer needed

#### Security

* Added priority to roles for default routes (#4331)
* New User Login trigger now provides effective roles (#3781)

### Bug Fixes

#### Admin Console

* Fixed an issue with job stats on the home page (#4342)
* Fixed an issue with the admin console link for non-administrator users in the portal (#4440)
* Fixed an issue with the API stepper (#4441)
* Fixed an issue expanding a git commit twice (#4430)
* Fixed an issue working with large git repositories (#4347)
* General performance improvements
* Fixed an issue editing C# files

#### Apps

* Fixed an issue loading app modules on Linux in some scenarios (#4025)
* Fixed an issue with background image stretching (#4269)
* Fixed an issue with the table toolbar when there is no data in the table (#3755)
* Fixed an issue with duplicate values in New-UDAutocomplete (#4454)
* Fixed an issue with editing columns and rendered cells in New-UDDataGrid (#2539)

#### Automation

* Fixed an issue with the Default Run On setting and computer groups (#4333)

#### Installer

* Fixed an issue with the installer and custom appsettings.json files during upgrades (#4393)

#### Module

* Fixed an issue with Get-PSUAppToken -Id (#4412)
* Fixed an issue with Grant-PSUAppToken (#4416, #4415)
* Fixed issue loading module in Windows PowerShell

#### Platform

* Fixed an issue deleting identities (#4332)
* Fixed an issue with psu cli's db migration tool to SQL (#4442)
* Fixed an issue with SQLite the docker container default settings (#4447)
* Fixed an issue where the login redirect would drop the query string (#4381)
* Fixed an issue with grooming certain database tables (#4361)

#### Portal

* Fixed an issue with the built-in widgets and scripts in folders

#### Security

* Fixed an issue with statically assigned nested roles (#4432)

## 5.3.3 - 2/24/2025

### Bugs

#### APIs

* Fixed an issue with event hub commands (#4406)

#### Automation

* Fixed an issue where the identity was not listed correctly when calling Invoke-PSUScript with an app token (#4414)
* Fixed an issue reading scripts from a UNC path (#4413)

#### Module

* Fixed an issue with Set-PSUAuthenticationMethod (#4421)

#### Tools

* Fixed an issue with psu CLI's db tool

## 5.3.2 - 2/18/2025

### Bugs

#### Cmdlets

* Fixed a critical security issue with the Universal module authentication. [(CVE TBD)](changelogs/cves.md#cve-tbd-2-18-2025-privilege)

#### Agent

* Fixed an issue with certain messages sent to event hubs (#4390)

## 5.3.1 - 2/17/2025

### Bugs

#### Admin Console

* Fixed an issue expanding the git commit table (#4368)

#### Apps

* Fixed an issue where the page icon would be duplicated
* Fixed a file encoding issue with pages (#4360)

#### APIs

* Fixed an issue calling Invoke-PSUScript in an API when Strict permission mode was enabled (#4367)

#### Automation

* Fixed an issue where jobs could be marked as failed after completing successfully
* Fixed an issue discovering test files in nested directories.

#### Cmdlets

* Fixed an issue with Invoke-PSUScript -Integrated (#4373)

#### Platform

* Fixed several issues git settings, changing remotes and cloning (#4369)

## 5.3.0 - 2/11/2025

### Features

#### Admin Console

* Added Rate Limits page (#4201)
* Updated to Ant Design 1.1 (#4060)
* Improved Script Folder Management (#3724)
* Process view now works in multi-node environments (#1705)
* Added memory and process ID to jobs page (#4305, #4304)

#### Apps

* Added -FormData to New-UDForm (#4196)
* Added -ClassName, -AnchorVertical, -AnchorHorizontal and a close button to Show-UDSnackbar (#3535)
* Added support for new line characters in New-UDButton -Text (#3665)
* Added -ShowLoading to New-UDIconButton (#3047)
* Added -ShowTime to New-UDDatePicker (#1809)
* Added -RadialBar to New-UDNivoChart (#3717)
* Added -LogoComponent to New-UDPage (#2803)
* Added command history to app debug console (#2194)

#### APIs

* Added Run As support to endpoints (#3068)

#### Automation

* Improved simple schedules (#4203)
* Schedules and triggers are now deleted when their script is deleted (#1979)
* Added computer groups to triggers run on settings (#3993)
* Added Pester test support (#2977)
* Added support for excluding scripts from the job tab (#4019)

#### Agent

* Added PSU\_AgentLogPath (#4232)

#### Cmdlets

* Improved Write-PSULog's default behavior (#4253)

#### Platform

* Added support for specifying NameIdFormat for SAML2 configurations (#4226)
* Added the ability to create app tokens without identities (#3185)
* Added reset admin password function to psucli (#4221)
* Optimized module discovery (#4247)
* Improved git error messages (#2027)
* Added support for loading SAML2 metadata (#3061)

#### Portal

* Unauthenticated apps are now displayed on the portal (#4258)

### Bugs

#### Admin Console

* Fixed an issue with git sync status display (#4215)
* Fixed sort order of scripts on the trigger modal (#4242)
* Fixed an issue with the UI on refreshing properly after an app was installed (#4228)
* Fixed issues with Rerun job button (#4209)
* Fixed an issue clearing DateTime parameters on schedules (#4208)
* Fixed an issue with the tags table reload (#4268)
* Fixed search on several pages (#4267, #4231)
* Fixed an issue with the Portal Resources page (#4291)
* Fixed an issue selecting nested folders for scripts (#4284)
* Fixed an issue running scripts with certain parameter set definitions (#4299)

#### Agent

* Fixed an errant warning in the agent log (#4265)

#### Apps

* Fixed an issue with the New-UDProgress in the dark theme (#3905)
* Fixed an issue where New-UDDataGrid did not display the first\last page buttons (#3973)
* Fixed an issue with Publish-PSUStaticApp
* Fixed an issue calling New-UDUpload multiple times with the same file (#4165)
* Fixed an issue with Start-UDDownload in external environments (#4273)
* Fixed an issue changing the year in New-UDDatePicker (#4230)
* Fixed an issue with New-UDTransferList -Enhanced (#4223)

#### APIs

* Fixed an errant warning log message in post APIs (#4252)
* Fixed an issue with secret variables in endpoints (#4301)
* Fixed an issue executing a C# API after a compilation error had occurred (#4214)

#### Automation

* Fixed an issue with Job Cancelled triggers not running (#4245)
* Fixed job log order (#4274)

#### Cmdlets

* Fixed an issue with the default parameter set on Set-PSUEvent (#4262)
* Fixed an issue with the deployment cmdlets (#4278)
* Fixed an issue with Stop-PSUJob (#4341)

#### Deployments

* Fixed the deployment download button (#4277)

#### Installer

* Fixed an issue where the MSI would log the service account password in clear text during install (#4246)

#### Platform

* Fixed an issue where git settings from appsettings.json would be used across a computers (#4261)
* Fixed an issue loading custom module information (#4254)
* Fixed an issue running the Memory Health Check on new versions of Windows (#4293)
* Fixed an issue setting the system log level
* Fixed an issue with DisableAutoReload (#4327)
* Fixed an issue using basic auth when Windows auth was enabled in IIS
* Fixed an issue where $RefreshToken was not available in apps when SaveTokens was set for OIDC (#4330)
* Fixed an issue accessing published folders by UNC path (#4339)
* Fixed an issue with psu git --disable-crl (#4164)

## 5.2.3 - 2/05/2025

### Bug Fixes

#### Installer

* Fixed issue with default service account password

## 5.2.2 - 1/29/2025

### Bug Fixes

#### CVE

* Fixed a directory traversal issue with Published Folders - [CVE-2025-26792](changelogs/cves.md#cve-2025-26792-1-29-2025-information-disclosure)

#### Admin Console

* Fixed an issue where Run As credential selector was not available on the Environments property dialog (#4298)

#### APIs

* Fixed an issue where Send-PSUEvent would attempt to send events to invalid groups (#4262)

#### Apps

* Fixed an issue where Sync-UDElement would not reset table selection state (#4257)
* Fixed an issue where reloading modules would cause apps to restart (#4241)
* Fixed an issue with New-UDSelect -DefaultValue and -Sx (#4169)

#### Cmdlets

* Fixed an issue where Get-PSUSchedule could throw an exception

#### Platform

* Fixed an issue authenticating against APIs with Basic credentials

## 5.2.1 - 1/19/2025

### Bug Fixes

#### Admin Console

* Fixed an issue clicking the help links in the admin console (#4237)

#### Apps

* Fixed an issue with New-UDMenuItem -Style and -Sx (#4219)

#### Automation

* Fixed an issue with Default Run On, computer groups and manually run jobs (#4244)

#### Cmdlets

* Fixed an issue calling Invoke-PSUScript -Script with the name of a script in a folder and not the full path

#### Platform

* Fixed an issue starting processes when the default environment had a credential set
* Updated Azure.Identity and Microsoft.Identity libraries to support the latest version of Az and Microsoft.Graph modules

#### Portal

* Fixed an issue rearranging portal widgets in the portal page editor

## 5.2.0 - 1/14/2025

### Features

#### Admin Console

* Added sorting to all tables in the admin console (#4137)
* Added security, telemetry, and license configuration to first time wizard (#3990)
* Added setting for configuring login page theme (#3978)
* Simplified Gallery page
* Added name and vault to the set secret value modal (#4174)
* Improved editing performance when PSScriptAnalyzer is enabled

#### Apps

* Added -Target to New-UDButton (#4134)
* Added -Sx and -Style to New-UDCardHeader and New-UDCardMedia (#4146, #4145)
* Added support for setting initial table state (#2779)
* Added support for Publish-PSUStaticApp
* Added app debugger tab
* Added -Network to New-UDNivoChart
* Added -Sx to New-UDTimeline and New-UDTimelineItem (#3804)
* App editor now includes IntelliSense for app module (#2082)

#### Agent

* Added 'PSU\_AgentLogLevel' environment variable to allow for controlling the log level.
* Added support for configuring agent with user-scoped settings location

#### Automation

* Added default Run On setting (#4116)

#### Portal

* Branding settings are now applied to the portal (#4119)

#### Platform

* Added support for managing PSResource repositories (#4106)
* Default admin password complexity is now a warning rather than an error (#4006)
* Added support for changing git repository and branch
* Improved extension module load behavior (#4141)
* Added support for managing vaults (#1470)
* Added account-based licensing (#2978)

### Bug Fixes

#### Admin Console

* Fixed an alignment issue with the Reload Configuration button (#4136)
* Fixed an issue displaying scripts in nested folders (#4127)
* Fixed an issue with Job Run Id (#4153)
* Fixed navigation issues in the admin console (#4158, #4162)
* Fixed an issue with displaying saved string array schedule parameters (#4144)
* Fixed an issue with the re-run job button (#4150)
* Fixed an issue adding computer tags multiple times (#4186)

#### Apps

* Fixed an issue running apps defined in modules
* Fixed an issue where all apps could reload when one changed (#4121)
* Fixed an issue when attempting to run blocked scripts (#3987)
* Fixed an issue with table row selection when using server side processing (#4000)

#### Automation

* Fixed an issue running jobs longer than 30 minutes when using PostgreSQL (#4177)
* Fixed an issue running jobs across all computers in a computer group

#### Cmdlets

* Fixed an issue with Get-PSUSchedule not returning the next execution time (#4168)

#### Installer (MSI)

* Fixed an issue with the desktop mode install

#### Platform

* Fixed an issue where psu.exe was missing from the installation media
* Fixed an issue with computer heartbeats in multi-node environments (#4167)

## 5.1.2 - 12/17/2024

#### Bug Fixes

Automation

* Fixed a performance issue retrieving jobs and data consistency issue when running jobs in parallel.

## 5.1.1 - 12/16/2024

#### Bug Fixes

#### Admin Console

* Fixed an issue with the log view not loading properly (#4129)
* Fixed an issue with Code Editor crashing (#4131)
* Fixed an issue with inconsistent and slow IntelliSense

#### Apps

* Fixed an issue with New-UDEndpoint -Schedule (#4130)

#### Agents

* Fixed an issue with agent reconnection (#4126)

#### Cmdlets

* Fixed an issue with Get-PSUCache -List (#4124)

#### Platform

* Fixed an issue groom idle terminal instances (#4138)

## 5.1.0 - 12/11/2024

#### Features

#### Admin Console

* Added -DarkAppBarLogo to New-PSUBranding (#3170)
* Added .gitignore editor to git page (#3560)
* Added configuration file reload dropdown (#3812)
* Table page sizes are now sticky (#4023)
* Added Nested Role field to roles property form.
* Added Import Secrets button (#4080)
* Added localized date time display to admin console (#3780)

#### APIs

* Added contact, license, version and terms of service to OpenAPI endpoint docs (#3900)
* Added -ResponseVariable to Invoke-PSUEndpoint (#4054)

#### Apps

* Added -JavaScript to New-UDEndpoint (#3121)
* Added support for enter key in prompts in apps (#3326)
* Added support for Read-Host -AsSecureString
* Added support for nested modals (#3163)
* Added Columns and SelectedRowIds to $EventData in -LoadData for New-UDTable (#3982)

#### Automation

* Child jobs not display parent schedule (#3373)
* Added support for copy\paste in terminals (#4096)

#### Platform

* Added -DefaultTokenLifetime to Set-PSUSettings and admin console (#2872)
* Added preview support for Deployments (#4101)

#### Portal

* Added support for SimpleSelect in Widgets

#### Tools

* Added psu.exe git command line tools
* Added psu.exe db migration command line tools

#### Bug Fixes

#### Admin Console

* Fixed an issue with the tab URLs updating incorrectly (#4062)
* Fixed an issue when creating secrets (#4074)
* Fixed a display issue with online licenses (#4068)
* Fixed an issue logging in with SAML2 from the login page (#4075)
* Fixed an issue displaying string arrays in schedule parameters (#4084)
* Fixed an issue with the copy button in the API tester in non-secure sites (#4108)

#### Apps

* Fixed an issue with the unauthorized page (#4065)
* Fixed an issue where the docs app would not load (#4067)
* Fixed an issue with favicons (#4055)
* Fixed an issue with dynamically registered components and Add-UDElement (#3585)
* Fixed an issue with Invoke-UDRedirect -OpenInNewWindow (#4104)

#### APIs

* Fixed an issue with the endpoint table (#4066)
* Fixed an issue with the endpoint tester and non-JSON values (#4098)

#### Cmdlets

* Fixed an issue where Get-PSUCache threw an exception rather than returning $null when the key was not found (#4078)

#### Automation

* Fixed an issue with Write-PSFramework and job logs (#4071)

#### Platform

* Fixed an issue loading the OpenTelemetry plugin in Docker (#4081)
* Fixed an issue where user sessions were groomed before the data retention setting (#4089)
* Fixed an issue with user scoped logging (#4103)
* Fixed an issue with the configuration file system watcher

#### Portal

* Fixed an issue with script table display (#4083)

## 5.0.16 - 11/18/2024

#### Admin Console

* Renamed Functions tab in app editor to Module
* Fixed an issue creating a CRON schedule on the script page (#4035)
* Fixed an issue with the Run button on the health checks page (#4024)
* Added Start Time, Created Time and Elapsed Time to the jobs table (#4028)
* Fixed an issue where form authentication was shown on the login page when disabled (#4041)
* Added reset branding button (#4030)
* Fixed an issue where non-persistent cache data had missing time stamps
* Added Available in Branch to UI
* Improved memory usage output on process page (#3828)
* Fixed an issue with the failed login configuration page
* Added variable value form (#4049)
* Fixed an issue where System would show in the permission identity selector (#4040)
* Fixed an issue where Reader role could execute scripts in admin console (#4061)
* Fixed an issue where the admin console could exhaust SQL connections (#4056)

#### APIs

* Added -Computer to Send-PSUEvent (Invoke-PSUCommand)
* Fixed an issue where variables were retained between invocations in a persistent runspace
* Fixed an issue executing endpoints that use -Module-Command (#4053)

#### Apps

* Added -Checkbox to New-UDSelect (#1996)
* Fixed an issue with New-UDAutocomplete -Multiple layout (#3756)
* Added -SortType numeric to New-UDTableColumn (#3837)
* Fixed an issue with -Locale in New-UDDatePicker (#4017)
* Fixed margin of UDTextbox with an icon (#4051)

#### Automation

* Fixed an issue scheduling the groom job past 59 minute intervals (#4031)
* Fixed an issue renaming schedules (#4034)

#### Module

* Fixed an issue where module help was not updating properly.
* Fixed an issue with Get-PSUCache -Key case sensitivity (#4043)

#### Portal

* Links now open in a new tab (#4027)
* Added disabled and roles settings for portal (#4037)
* Fixed an issue with portal authentication redirects (#4010)

#### Platform

* Fixed an issue grooming jobs when using PostgreSQL (#4032)
* System log level can now be set in the admin console

## 5.0.15 - 11/5/2024

#### Admin Console

* Fixed an issue with tagged variables (#4002)
* Added Telemetry option to General Settings
* Added Report Bug button to error alert
* Added tooltip help to maintenance mode and readonly mode for computers (#3996)
* Added Help menu
* Documentation links now open in a new tab
* Fixed an issue with job execution time (#4016)
* Reduced Blazor log level
* Fixed an issue when jobs had multiple requests for feedback

#### APIs

* Fixed an issue where event hub agent would not log Write-\* calls (#3983)
* Added -RemoteDomainName and -RemoteUserName to Get-PSUEventHubConnection (#4009)
* Fixed an issue where event hubs would only run one command at a time (#3988)

#### Apps

* Fixed an issue with button colors (#3974)
* Fixed an issue where apps would auto-deploy when secrets were changed (#4022)

#### Automation

* Fixed an issue grooming jobs (#3929)

#### Cmdlets

* Added -Integrated mode for cmdlets
* Added -Silent to Invoke-PSUScript and Wait-PSUJob
* Fixed an issue with switch parameters and Invoke-PSUScript (#4011)

#### Platform

* Fixed an issue where the service could crash when losing database connection (#4012)
* Fixed an issue where secrets could be deleted in multi-node environments during git sync (#3959)

## 5.0.14 - 10/31/2024

#### Admin Console

* Fixed an issue where a custom app bar logo would not display (#3945)
* Fixed an issue pressing the tab key in the debug console (#3939)
* Added support for deleting computer tags (#3961)
* Fixed an issue starting an app that was in a start failed state (#3965)
* Added Reload Configuration Files button to the Configuration Files page
* Fixed an issue where nodes in git merge conflict status would not display state properly (#3971)
* Added file editor to apps and modules pages
* Fixed an issue with additional info buttons on home page in nested sites (#3979)
* Fixed a display issue with endpoint methods (#3975)
* Fixed an issue editing scripts and view jobs when using Windows Auth and PostgreSQL (#3952)
* Added secret value form (#3954)
* Fixed an issue where readonly endpoint wouldn't expose the test or log tabs (#3947)
* Fixed an issue with job execution time when using PostgreSQL (#3915)
* Added Auto Deploy option to app settings (#3992)

#### Apps

* Fixed an issue where a button group drop down item would not be shown when used within a modal (#3765)

#### API

* Fixed an issue with requests timing out too early (#3946)
* Fixed an issue with an erroneous error message with integrated APIs (#3955)
* Fixed an issue where endpoint docs wouldn't include base path (#3958)
* Fixed an issue with endpoint logging (#3950)
* Fixed an issue where remote server would not be indicated in event hub connections (#3980)
* Added -Active, -Hub, -RemoteComputerName, -ServerComputerName to Get-PSUEventHubConnection (#3981)

#### Platform

* Fixed an issue with configuration files reloading unnecessarily during git operations (#3956)
* Fixed an issue where a module PSM1 file could be locked when updating the content (#3948)

#### Portal

* Fixed an issue loading resources on the portal when using Windows Authentication (#3962)

#### Cmdlets

* Fixed an issue with Invoke-PSUEndpoint (#3969)

## 5.0.13 - 10/22/2024

#### Admin Console

* Fixed an issue where dynamic parameter wouldn't update properly when other parameters changed (#3843)
* Added Permissions to role properties (#3931)
* Fixed an issue where the API tester incorrectly replaced route variables (#3937)
* Improved feedback of developer license usage
* Fixed an issue with app debugging

#### Apps

* Fixed an issue rendering static tabs (#3928)
* Fixed an issue where Show-UDModal would throw errors (#3930)
* Fixed an issue with favicons and a base URL of / (#3873)

#### Automation

* Fixed scheduling a script against a computer group with a space in the name (#3927)
* Fixed an issue when scheduling scripts with the same name but different paths
* Fixed an issue loading scripts in nested folders that had differing names and paths

#### Cmdlets

* Improved certificate error information

## 5.0.12 - 10/18/2024

#### Security

* [Critical security fix for admin console ](https://docs.powershelluniversal.com/changelogs/cves#cve-tbd-10-17-2024-privilege-escalation-and-information-disclosure)(CVE-2024-50616)

#### Admin Console

* Fixed an issue with the back button on several pages (#3876)
* Fixed an issue with the tree view in the scripts page
* Fixed an issue adding secret variables (#3918)
* Fixed an issue where the incorrect execution was displayed for running jobs (#3915)
* Fixed an issue where the git status of only the current node would be shown (#3921)
* Fixed an issue with the display of nested jobs

#### API

* Fixed an issue where the swagger UI would default to schema rather than example (#3913)

#### Apps

* Removed the need to call Invoke-UDEndpoint with -Session for it to work (#2139)
* Fixed an issue where the tooltip arrow did not match the background color (#3580)
* Fixed an issue where the icon property in the page properties wouldn't persist (#3924)

#### Automation

* Fixed an issue scheduling scripts against computer groups (#3768)
* Fixed an issue running triggers when on trigger was missing the trigger script

#### Platform

* Fixed an issue where the Conflicting Modules health check could show conflicting information (#2850)

#### Security

* Fixed an issue logging in with Windows Authentication in IIS (#3916)

## 5.0.11 - 10/15/2024

#### Admin Console

* Fixed an issue updating the logging target file path (#3882)
* Fixed an issue saving non-PowerShell files in the Settings \ File editor (#3886)
* Added copy button to variables page (#3870)
* Fixed an issue with date time zone conversion when using PostgreSQL
* Added missing Identity page.
* Fixed an issue with the Show Streams and Show Timestamp buttons (#3902)
* Added log tab to roles page (#3896)
* Fixed an issue modifying module content (#3849)
* Fixed vertical sizing of code editor (#3883)

#### APIs

* Fixed an issue where swagger docs could crash the browser (#3877)
* Fixed an issue when editing endpoint files on disk (#3869)
* Fixed an issue specifying arrays of custom types with OpenAPI docs (#3874)
* Fixed an issue with nested IIS site and Swagger UI (#3867)

#### Apps

* Fixed an issue with apps that have a space at the end of the name (#3891)

#### Automation

* Fixed an issue where Invoke-PSUScript could cause job status to be stuck in "Running" state. (#3845)
* Fixed an issue where DateTime parameters without a value were set to an empty string in Schedules (#3893)

#### Platform

* Fixed server startup performance when the database has a large number of jobs
* Fixed an issue with schedule configuration files updating when they should not be (#3885)
* Improved performance of configuration file database queries
* Improved performance of database updates
* Fixed an issue when renaming or deleting environments (#3897)
* Added $PSUGitBranch automatic variable (#3909)

## 5.0.10 - 10/7/2024

#### Admin Console

* Fixed an issue where job search was case-sensitive (#3835)
* Fixed horizontal scrollbar on claim information table (#3834)
* Fixed an issue filtering jobs by multiple statuses (#3833)
* Fixed date time display
* Fixed issue with endpoint tab (#3848)
* Fixed an issue with script documentation editor (#3862)
* Added reset settings button to My Identity page (#3863)
* Fixed issue saving endpoint docs and tags (#3866)

#### APIs

* Fixed an issue with OpenAPI docs default value for properties (#3430)
* Fixed an issue with endpoint path format (#3838)
* Fixed an issue calling endpoints with Windows authentication (#3858)
* Fixed an issue with the view docs button in a nested IIS site

#### Apps

* Fixed an issue with nested table rendering and overall table performance
* Fixed a performance issue when loading and saving apps (#3809)
* Fixed an issue with New-UDForm -Script (#3854)

#### Automation

* Fixed an issue with PSCredential parameters (#3864)

#### Cmdlets

* Fixed an issue where valid certificates could be rejected by the cmdlet transport layer
* Improved gRPC errors (#3830)

#### Platform

* Fixed an issue where saving schedules could cause changes to parameter positions resulting in unnecessary file changes (#3847)
* Fixed an issue with database logging
* Configuration file resources are now sorted deterministically (#3857)
* Windows PowerShell 5.1 now targets .NET 4.7.2 to support the PartnerCenter Module (#3855)

#### Portal

* Fixed an issue editing Portal widgets (#3839)

#### Security

* Fixed an issue signing out of WS-Federation (#3861)

## 5.0.9 - 9/30/2024

#### Admin Console

* Fixed an issue working with array variables (#3802)
* Fixed an issue with the job list in a script's page (#3816)
* Fixed a UI issue with Enhanced Token Security (#3783)
* Fixed tree view scrolling for files (#3819)
* Improved feedback of the start\stop button for apps.
* Fixed issue with schedule search (#3813)
* Fixed an issue displaying date and time in the proper client time zone (#3753)
* Fixed an issue where the console would flash when in light mode
* Fixed an issue with one-time schedule time zones
* Fixed an issue where the console would show the license paywall when reloading pages in certain configurations (#3725)
* Fixed an issue when navigating directly to the scripts page when using SQL server and Windows Authentication (#3731)

#### Automation

* Fixed an issue running a script manually on a target node (#3818)
* Fixed an issue with scheduling scripts against computer groups
* Fixed an issue running one-time schedules in multi-node environments (#3784)

#### APIs

* Fixed an issue with Send-PSUEvent not being implemented in certain invocation methods (#3810)

#### Apps

* Fixed an issue loading data in New-UDDataGrid
* Fixed an issue with -IdentityColumn in New-UDDataGrid (#3832)
* Fixed an issue with Nivo chart tool tips (#3718)
* Fixed an issue with labels for New-UDNivo -Chart Bubble (#3719)

#### Module

* Improved the error message when attempting to create a schedule for a script that doesn't exist (#3824)

#### Platform

* Fixed an issue where improperly formatted configuration scripts would cause issues with the platform (#3800)
* Fixed an issue with redirection after login in when using a Linux docker container
* Fixed an issue with log file configuration (#3261)

## 5.0.8 - 9/23/2024

#### Admin Console

* Improved scrolling of git commits table (#3741)
* Fixed an issue with the Discover Environments button in Two Way Automatic git sync mode
* Added the ability to clear the Run In, On and As dialogs for schedules (#3772)
* Fixed an issue where computer groups did not display the (Any)(All) specifier and would only run on 1 node in the group (#3770)
* Fixed an issue with JavaScript caching between versions of the admin console (#3774)
* Child jobs are now shown as a nested table in the jobs page (#3767)
* Fixed issue with file parameters for scripts (#3778)
* Fixed an issue where computer group tags were not populated in the computer group dialog (#3771)
* Fixed an issue filtering API endpoints by documentation (#3642)
* Endpoint search now adds the search to the query string (#3643)
* Added search to schedule page (#3785)
* Fixed an issue where clicking on a script name in a job details page wouldn't navigate to the script (#3787)
* Added the schedule buttons to the scripts page (#3785)
* Fixed an issue with display app token expiration date (#3782)
* Extended the width of the script filter for the jobs table (#3795)
* Fixed validation in the reset password dialog (#3793)
* Fixed an issue where IntelliSense in the editor would overwrite content past the autocomplete suggestion (#3758)
* Fixed an issue where you could not set the value of secrets in one-way git sync (#3792)
* Added error stack trace to error tab in jobs page (#3807)
* Added color indicator to filters in the jobs page (#3805)
* Fixed an issue clearing the script filter for the jobs table (#3806)

#### Apps

* Fixed an issue with New-UDFloatingActionButton not staying in the bottom right corner of the screen. (#3720)
* Fixed an issue with intermittent runspace errors on startup (#3777)
* Improved startup performance and memory usage.
* Fixed an issue with apps running under Windows PowerShell 5.1 (#3801)

#### Automation

* Fixed an issue where Wait-Debugger wouldn't trigger the debug console in the Integrated environment (#3803)

#### Module

* Fixed an issue receiving large data from the server (#3775)

#### Platform

* Fixed an issue checking for updates
* Fixed an issue pushing to git remote using SSH keys (#3729)
* Fixed issue pausing git sync when set through appsettings.json (#3766)
* Fixed an issue where PSU would start slowly when many modules were installed in the Repository directory (#3790)
* Fixed an issue where the Missing Environment health check would fail for Universal.Agent

#### Security

* Fixed an open redirect issue (#3763)
* Fixed an issue with Windows authentication and authorization in the admin console (#3776)

## 5.0.7 - 9/16/2024

{% hint style="info" %}
This update adds an index to the database. If your service fails to start in a timely manner during the install, you may need to run a [manual schema update](https://docs.powershelluniversal.com/config/persistence#manual-schema-install-update).
{% endhint %}

#### Admin Console

* Fixed an issue where computer groups weren't displayed in the Run On dropdown.
* Fixed an issue where DateTime parameters would not display the time portion of the selector
* Fixed an issue creating nested folders (#3723)
* Fixed an issue displaying schedules that do not include a computer but have a custom environment (#3721)
* Library has been renamed to Gallery to align with other nomenclature
* Fixed an issue where users logging in with a non-admin user would redirect to /admin rather than /portal
* Fixed issue autocompleting paths in the editor (#3726)
* Added a Not Authorized page, rather than a blank page, when a user tries to access a page, they do not have access to (#3735)
* Added confirmation dialog when navigating away from a page with unsaved changes (#3737)
* Added missing Startup Script and Process Startup Script controls to the environment properties modal (#3748)
* Fixed an issue displaying the default value for scripts in the run and schedule dialog (#3752)
* Fixed an issue displaying string array types in the run and schedule dialog (#3751)
* Fixed an issue where PowerShell Universal could crash when loading large job output in the admin console (#3745)
* Improved performance of job output in the admin console

#### Agent

* Added global exception handling and logging for the agent process

#### APIs

* Added /api/v1/first-run endpoint to set first run settings (#3749)

#### Apps

* Fixed an issue where apps would not start when using pwsh.exe (#3732)
* Fixed an issue where Set-UDElement did not work with UDExpansionPanel (#3626)

#### Automation

* Fixed an issue with schedule parameters
* Added DateOnly and TimeOnly parameter selectors
* Fixed an issue where long-running jobs would spawn a new job after some time (#3709)
* Added indices to the JobOutput table to improve performance

#### Module

* Invoke-PSUScript -Name is now more flexible to relative paths (#3727)
* Fixed an issue with New-PSUSchedule when changing parameter names of the target script
* Fixed an issue with TrustCertificate in appsettings.json
* Fixed an issue where license cmdlets were not implemented properly (#3738)

#### Portal

* Fixed an issue setting nullable bool attributes in PSBlazor

#### Platform

* Fixed an issue with Windows PowerShell $Env:PSModulePath (#3728)
* Modules are now installed in a background job to avoid long delays in the UI

#### Security

* Fixed an issue where certain APIs would not work when SAML2 was enabled (#3739)

#### Tools

* Fixed an issue migrating terminal history with psudb.exe

## 5.0.6 - 9/9/2024

#### Admin Console

* Fixed an issue where the git pause switch wouldn't display the proper status when paused (#3688)
* Added delete computer button for offline computers (#3693)
* Improved display of charts on dashboard
* Fixed property label text wrapping in modal dialogs in the admin console (#3703)
* Improved admin portal page header formatting (#3704)
* Fixed an issue where the Discover Environments button would be enabled when git sync wasn't editing (#3714)
* Fixed an issue where editing git settings when using SQL would cause it to delete the settings (#3688)
* Fixed a display issue with the job feedback modal (#3692)
* Fixed the performance of the schedules page (#3659)
* Added missing Diagnostics button

#### APIs

* Fixed an issue calling Invoke-PSUScript in an unauthenticated API using the permissive security policy

#### Automation

* Fixed a SQLite locking issue when running many jobs at once
* Fixed an issue calling Invoke-PSUScript -Name with a path (#3708)

#### Apps

* Fixed an issue calling OnRender in OnRowExpand in New-UDTable (#3695)
* Fixed an issue calling Invoke-PSUScript in apps using the permissive security policy
* Fixed an issue with a base URL of / and the admin console routing (#3711)
* Fixed an issue where duplicate apps could show up after server restart (#3706)
* General fixes to Nivo Charts (#3682, #2083)

#### Platform

* Fixed an issue with redirect URL after login (#3694)
* Added support for configuring -TrustCertificate flag at the server level (#3697)
* Fixed an issue where variables stored in database would be null after restart (#3701)
* Removed 4MB limit for Universal cmdlet calls (#3700)
* Fixed an issue with psudb.exe where it could throw an exception attempting to move job output
* Fixed an issue with background job scheduling when using multi-node configurations
* Added -Migrate to psudb.exe to enabling migration to the newest schema in SQLite
* Fixed an issue where upgrades from v4 with New-PSUEnvironment -EnableDebugger would cause the environment to not show up (#3712)
* Fixed an issue where git sync would push even when there were no changes (#3713)

#### Portal

* Fixed an issue where an error could be displayed on the portal for certain authentication types

#### Security

* Updated .NET (8.0.8) and PowerShell (7.4.5) SDK versions to address security issues in dependencies
* Added missing View Claim Information button
* Fixed an issue enabling Anonymous Authentication and Windows Authentication in IIS (#3715)

## 5.0.5 - 9/3/2024

#### APIs

* Fixed an issue where endpoint content wouldn't be displayed in the admin console when using -Path
* Fixed an issue changing the path of endpoints (#3685)

#### Apps

* Fixed an issue where -DisableAutoStart had no affect (#3658)
* Fixed issue with -OnClick and -Theme on New-UDNivoChart (#3667)
* Added icon selector to page properties (#3678)
* Fixed an issue where a blank file and folder would be created if the app pointed to a path that didn't exist (#3679)
* Fixed an issue where installing apps from the library wouldn't show up (#3686)

#### Automation

* Added missing trigger schedule button

#### Platform

* Fixed an issue where the computer page would incorrectly show an error about the number of licensed computers.
* Fixed an issue where changing branding would duplicate lines in branding.ps1 (#3666)
* Fixed an issue with psudb.exe failing to convert jobs in certain configurations (#3670)
* Added permissive security model to cmdlets (#3676)
* Display number of selected changes in git commit (#3645)
* Fixed an issue where secret variable values would not be deleted from the database (#3654)
* Added missing clear cached claims button on the roles page.
* Fixed an issue running Connect-AzAccount

## 5.0.4 - 8/28/2024

#### Platform

* Fixed an issue loading custom health checks

#### Security

* ❗Fixed an issue where First Run dialog could be called multiple times

## 5.0.3 - 8/28/2024

#### Automation

* Fixed an issue displaying the scripts page

#### Apps

* Fixed a license expiration issue with data grids and date\time pickers

## 5.0.2 - 8/27/2024

#### Apps

* Fixed an issue with displaying non-authenticated apps (#3641)

#### Automation

* Fixed an issue with scheduling on Windows Server 2016 (#3647)
* Fixed an issue with script folder display (#3639, #3660)
* Fixed an issue where the Time Zone selector was missing for schedules (#3649)
* Added missing list view for scripts (#3635)
* Fixed an issue where the inline debugger wouldn't trigger in the integrated environment (#3622)
* Fixed an issue where schedule parameters would not display

#### Portal

* Fixed issue with parameter sets on the portal (#3617)

#### Platform

* Fixed issue with license enforcement in the admin console
* Fixed an issue where the agent would give up retrying to connect after some time (#3614)
* Fixed an issue with psudb.exe throwing an exception then migrating app tokens and jobs (#3652)
* Improved performance of psudb.exe
* Fixed an issue where disabling Windows Auth would cause users to fail to login until cookies were deleted (#3648)
* Fixed an issue where the platform would attempt to use powershell.exe, if configured
* Fixed an issue changing Script Base Path when API Base Path was already set (#3651)
* Fixed a locking issue with SQLite databases
* Fixed issue copying app tokens on HTTP servers (#3655)
* Improved connection logic in cmdlets to support more server configurations
* Fixed an issue with the online license activation retry failing

## 5.0.1 - 8/23/2024

#### APIs

* Fixed an issue when viewing endpoint documentation (#3607)
* Added event hub connections table
* Fixed an issue with Send-PSUEvent and -Parameters
* Fixed an issue with the endpoint tester and nested IIS sites (#3611)
* Added endpoint search (#3631)

#### Apps

* Fixed issues with the Pages tab in the app editor
* Live docs menu item now opens in a new tab
* Fixed an issue with New-UDTransferList (#3634)
* Fixed an issue with a New-UDDataGrid example

#### Automation

* Fixed an issue with job output appearing out of order

#### Platform

* Reduced the default System Log Level from Debug to Information
* Fixed an issue with environment discovery and Windows PowerShell 5.1
* Improved error reporting when jobs fail to start
* Fixed an issue with the configuration file editor (#3603)
* Fixed an issue with Universal cmdlets and HTTP
* Fixed an issue with SQLite v4 to v5 database update
* Fixed an issue logging in with SAML2 (#3623)
* Fixed an issue with home page formatting (#3620)
* Added select all button to the git commit page (#3584)
* Fixed a theme issue with the permission drawer (#3618)

## 5.0.0 - 8/20/2024

{% hint style="warning" %}
Please review the [upgrade documentation](getting-started/upgrading.md) before updating your environment.
{% endhint %}

#### Breaking Changes

* Removal of Pages
* Removal of Desktop mode
* Removal of App Designer
* Removal of LiteDB support

#### APIs

* Added endpoint tester
* Added support for string array query string parameters
* Added -ApiBaseFolder to Set-PSUSettings

#### Automation

* Added support for selecting streams when running a script manually
* Added Hide Run Later
* Added Quick Run button
* Added in-line debugger
* Extended job filtering to include all columns
* Added support for dynamic parameters
* Added -Tags to Invoke-PSUScript
* Added -HideChildren, -HideTriggered, -HideScheduled to Get-PSUJob
* Added a page to view jobs for a schedule
* JobRunId has been promoted from an experimental to a full feature
* Added support for script documentation

#### Apps

* Added -Path to Start-UDDownload
* Added -Sx to New-UDBadge
* Added -RemoveMargin to New-UDCard
* Added -SelectedTabIndex to New-UDTabs
* Added -Enhanced to New-UDTransferList
* Added -DisableArcLinkLabels and -DisableArcLabels to New-UDNivoChart
* Added module support for apps

#### Portal

* Added preview version of Portal
* Added Portal Page designer
* Added Portal Widget editor

#### Platform

* Added New Blazor-based Admin Console
* Updated to .NET 8.0 and PowerShell 7.4
* Added opt-in telemetry collection
* Get-PSUCache now returns the entire cache item information
* Added custom PSScriptAnalyzer rule to check for built in variable usage.
* Added a first run setup to set the default admin user name and password
* Added support for role-based access with PSUCache
* Added password complexity and expiration enforcement
* Added support for module variables
* Added Password and KeySize to appsettings.json to configure AES 256 database secrets
* Added stack traces to notifications
* Added support for Emoji favicons
* Added support for discovering Python environments
* Added PSUDefaultAdminPassword and PSUDefaultAdminName environment variables
* Added granular permissions throughout the platform
* Implemented gRPC cmdlets across the platform
* Added a process that checks for module updates
* Added a health check that verifies an environment exists
* Added tags for variables
* Added PostgreSQL Support
* Added Script Library
* Added an option for updating git submodules during a pull
* Added Pause Git Sync button
* Added configuration settings for the loading page
* Added a page to view all tagged resources
* Added support for uploading to Published Folders
* Added support for database cache
