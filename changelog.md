---
description: Changelog for PowerShell Universal.
---

# Changelog

## 4.2.19 - 4/22/2024

#### APIs

* Fixed an issue where swagger types could show up in multiple documents (#2830)
* Fixed an issue with OpenAPI types in Swagger documents (#2948)
* Fixed an issue with authenticated OpenAPI docs and JWT tokens
* Fixed an issue with OpenAPI docs not reloading types properly (#3193)
* Fixed an issue using tabs in OpenAPI docs (#3180)
* Added error messages when OpenAPI docs fail to load

#### Automation

* Added -InformationAction and -ErrorAction support for Invoke-PSUScript -Wait
* Added script name to the Script \ Jobs page to support nested jobs (#3272)
* Fixed an issue where showing the timestamp in a job log would cause an error (#3277)
* Fixed an issue where canceled job could get stuck in cancelling state even after a server restart (#3164)

#### PowerShell Apps

* Fixed an issue where scheduled endpoints would not run properly (#3273)
* Fixed an issue using -OnRowStyle, OnRowExpand and -LoadData with New-UDTable (#2848)

#### Platform

* Setting git sync interval to 0 will now disable the automatic sync (#3232)
* Fixed an issue with proxy configuration
* Fixed an issue where Remove-PSUVariable would not work in -Integrated mode (#3281)
* Fixed an issue with logs for roles (#3227)
* Fixed an issue with log entry timestamp display in the admin console

## 4.2.18 - 4/15/2024

#### APIs

* Fixed an issue where the endpoint doc page didn't have an authorize button (#3262)

#### Automation

* Fixed an issue viewing job log files.
* Changed the language of the Jobs run stat on the homepage (#3235)
* Fixed an issue where Wait-PSUJob could throw an error based on job output (#3260)
* Fixed an issue where the Get-PSJobOutput cmdlet returned a different data format in v4.2.16 (#3259)

#### PowerShell Apps

* Fixed an issue with how memory usage was reported (#3217)
* Fixed an issue with $Query scoping (#3267)
* Fixed an issue with New-UDTextbox object result formats (#2838)

#### Platform

* Fixed an issue with variables stored in the database (#3250)
* New PSU versions are now automatically published to WinGet
* Fixed Set-PSUCache example (#3265)
* Fixed a display issue with app token expiration (#3097)
* Fixed an issue where $UserInfo was not defined in role scripts when using Okta (#3241)

## 4.2.17 - 4/8/2024

#### Automation

* Fixed an issue with Wait-PSUJob and Get-PSUJobOutput (#3249)
* Fixed an issue where jobs may be cancelled if Hangfire reset server status between heartbeats

#### Platform

* Fixed an issue with the logging documentation link (#3236)

## 4.2.16 - 4/5/2024

#### Automation

* Fixed an issue with computer maintenance mode (#3198)
* Fixed a performance problem with job logs in SQL

#### PowerShell Apps

* Fixed an issue with New-UDDataGridColumn code completion (#3147)
* Fixed an issue with -TimeZone on New-UDTimePicker and New-UDDatePicker (#3126)
* Fixed an issue with spacing of icons in New-UDList (#3173)
* Added -Style to New-UDTransition (#2836)
* Fixed a JavaScript error with New-UDTable (#3234)
* Added -MaximumLength to -New-UDTextbox (#3239)

## 4.2.15 - 3/28/2024

#### Automation

* Fixed an issue with Invoke-PSUScript -Wait and Wait-PSUJob (#3226)

#### APIs

* Fixed an issue where roles weren't displayed in the API Docs or the Event Hub modal (#3194)

#### PowerShell Apps

* Added -Hide to New-UDDataGridColumn (#3213)
* Fixed an issue with New-UDDataGrid -ShowQuickFilter and wildcards (\*) (#3211)
* Added -DefaultSortDirection example to docs for New-UDTable (#3216)
* Fixed an issue where apps could be duplicated in multi-node SQL setups (#3102)

#### Platform

* Fixed an issue with displaying git commit timestamps (#3206)
* Added an error message when the database encryption key was missing (#3222)

## 4.2.14 - 3/22/2024

#### APIs

* Fixed route matching for variable routes that also match static routes (#3181)

#### Automation

* Fixed an issue where app tokens could duplicate due to schedules
* Fixed an issue with the Hide Run As setting (#3187)
* Fixed a performance issue with writing job logs to SQL (#3200)
* Fixed an issue with calling Get-Acl (#2482)
* Fixed an issue loading Microsoft.PowerShell.Utility (#2423)

#### Apps

* Fixed an issue where -Style wouldn't apply when using -Disabled with New-UDCheckbox (#2144)
* Fixed an issue where the $Query hashtable was case sensitive (#3169)
* Added -Views to New-UDDatePicker (#2005)
* Fixed an issue with a stepper with no steps (#3188)
* Fixed an issue with the docs app stopping when editing other apps (#3174)

#### Platform

* Pinned to the Az.Accounts 2.12.5 version to avoid breaking changes in the module container image
* Fixed an issue with manually reloading dashboards.ps1
* Fixed documentation links (#3178)
* Removed manual garbage collection that could cause a service hang
* Fixed an issue with creating file system items in Linux (#3136)
* Fixed an issue with the Disabled Drives option for Disk Space Health Check (#3137)
* Encrypted git token\password in database (#3182)
* Fixed an issue with storing the git repository in the database (#3127)
* Fixed an issue with installing modules on a nested IIS site (#3186)
* Fixed an issue with computers being marked offline (#3197)
* Added computer name to notifications in multi-node setups (#3195)
* Computers are now listed under computer groups (#3196)

## 4.2.13 - 3/6/2024

#### API

* Fixed an issue where gRPC commands and endpoint could fail when a proxy was configured (#3086)
* Added logging to event hub client (#3114)

#### Apps

* Added -PaperStyle to Show-UDModal (#2832)
* Fixed an issue where -Sx would not apply to New-UDTooltip (#3095)
* Added -ValueOptions to New-UDDataGrid
* Fixed an issue where when a PSU node was stopped, apps would stop on all other running nodes (#3119)
* Fixed an issue where nested navigation more than one level deep would not expand when navigating to a page (#3107)
* Fixed an issue with duplicate app pages and deleting app pages (#3120)
* Fixed an issue where page icons might not be shown in the header (#3105)
* Fixed an issue where New-UDRadioGroup -Label would have no affect (#3111)

#### Automation

* Fixed an issue where $Job.Script was null in triggers (#3087)
* Added support for -InformationAction on Invoke-PSUScript.
* Improved performance when loading many scripts at startup (#2859)
* Fixed an issue where an invalid app token could be selected when running scripts.
* Fixed an issue where the job page could throw a JavaScript error in the admin console (#3109)
* Fixed an issue where default values for DateTime objects would not be honored in the admin console schedules (#2802)
* Fixed an issue where Get-PSUJob wouldn't work in Windows PowerShell with certain parameter sets (#3138)
* Fixed an issue where One Time schedules would not survive a restart in SQL (#3135)

#### Platform

* Fixed an issue where resources in read-only regions could be duplicated (#3082/#3090)
* Fixed a race condition with module discovery that could cause inconsistent IDs and duplicate modules (#3088)
* Fixed an issue where the version field would be empty on the computers page (#3089)
* Fixed an issue when displaying large variable values (#3074)
* Fixed an issue where Computer Groups would not show in the admin console (#3101)
* Fixed an issue where INSTALLPATH wasn't honored when specified on the command line of the MSI (#1494/#3028)
* Fixed an error deleting app tokens in the groom job
* Fixed an issue where git bundles would not work with SQLite (#3108)
* Fixed an issue where computers could fail to delete (#2812)
* Fixed an issue where the ARM64/v8 docker image had the wrong platform set (#1024)
* Fixed an issue launching PSU from the Okta dashboard when using SAML2
* Fixed an issue were a service in a multi-node setup may not start when upgrading (#3103)

## 4.2.12 - 2/1/2024

#### APIs

* Fixed an issue with nested IIS sites and the API tester with variables (#3051)
* Fixed an issue where syntax errors in endpoint docs would cause them to disappear from the admin console (#3056)

#### Apps

* Fixed an issue where New-UDChartJS would ignore -Options when using -Line (#2871)

#### Automation

* Added Set-PSUSchedule (#3055)
* Fixed an issue where Max Job Memory would roll over if set above 2GB causing all jobs to terminate
* Fixed an issue updating a terminal (#3070)
* Fixed an issue where jobs could be stuck in a running state after finishing successfully

#### Platform

* Fixed an issue where $UserInfo would be $null when using Auth0 and OIDC
* Fixed an issue where basic auth wouldn't correctly apply claims to the user
* Added better reporting of when the admin console is disabled
* Fixed an issue where configuration files would re-load twice when saved
* Fixed an issue where New-PSUVariable wouldn't correctly create PSCredential's in some circumstances
* Fixed an issue where disabling Local Account in an identity wouldn't change the status (#3077)
* Fixed an issue where identities could duplicate when using SQL persistence (#3054)

## 4.2.11 - 1/22/2024

#### API

* Fixed an issue where APIs could only return a maximum of 4MB of data when using an external environment

#### Automation

* **CRITICAL:** Fixed an issue where the Server Started trigger could cause PowerShell Universal to fail to start (#3065)

## 4.2.10 - 1/20/2024

#### APIs

* Fixed an issue where $ClaimsPrincipal would be $null in endpoints when using Basic authentication
* Fixed an issue where swagger documentation would show required if Mandatory was set to false (#3040)

#### Apps

* Status Description is now displayed when using Write-Progress in an app (#2768)
* Fixed an example in the New-UDDatePicker documentation (#3041)
* Fixed an issue with $AppFullUrl when using HTTPS with the default port (#3013)
* Fixed an issue where New-UDAutocomplete with empty options would return a JavaScript error
* Fixed an issue where New-UDDatePicker would not always send a DateTime object
* Fixed an issue where a UDTransferList with no items would display a JavaScript error (#3048)

#### Automation

* Added -RandomDelayMaximum to New-PSUSchedule (#2886)
* Added $Job variable to the Job Timed Out trigger (#2704)
* Fixed an issue where One Time schedules would be deleted before run when using One-Way Git Sync and SQL persistence
* Fixed an issue where canceling a job could result in an exception and the job becoming stuck in a canceling state
* Fixed an issue where the job status sort and filter icons would overlap (#2893)
* Fixed an issue where jobs would still run on computers in maintenance mode (#3034)
* Fixed an issue where jobs listed on a script page wouldn't link properly to a JobRunId (#2852)

#### Platform

* Retrying module lookup during startup when it fails due to an internal PowerShell state (#2813)
* Added Run Schedule and Job Diagnostics to the admin console when git one-way and manual mode are enabled (#3032)
* Fixed an issue where -SessionTimeout for New-PSUSetting would not be applied (#2914)
* Fixed an issue where the login page logo would fail to load over HTTP (#3037)
* Fixed an issue where health checks wouldn't be shown on the home page in some cases (#3043)
* Added PowerShell Universal version to the computer table (#3050)
* Removed license check for installing modules from the PowerShell Gallery
* Fixed an issue where updates to authentication methods could update the wrong method and cause authentication to fail (#3033)

## 4.2.9 - 1/10/2024

#### APIs

* Added Event Hub Client installer (#3003)

#### Apps

* Fixed an issue where the New-UDButton -Loading would not display properly in the dark theme (#2875)
* Fixed an issue where the UDApp variable is null (#3014)
* Fixed an issue where the create page dialog would clear on refocus (#2725)
* Fixed an issue where $AppFullUrl would not be correct for nested IIS sites (#3013)
* Fixed an issue where refreshing a Dynamic with a Table with an ID wouldn't refresh the table data (#2782)

#### Automation

* Fixed an issue expanding errors in the admin console (#3017)
* Fixed an issue where Reader and Execute roles could view the contents of a script by typing in the URL
* Improved the performance of the schedules page when using SQL persistence.
* Fixed an issue where retried jobs would queue forever when using SQL persistence
* Added HangfireWorkerCount configuration option to appsettings.json

#### Platform

* Fixed an error the groom job could fail clearing child jobs when using LiteDB (#3021)
* Added support for local files as admin console login page logos (#2705)
* Fixed warnings on server startup (#3023)
* Libgit2sharp now logs to the system log (#3026)
* Filters for health checks in the admin console (#3016)
* Fixed an issue where Get-PSUComputer -Integrated would return a gRPC error when using SQL persistence (#3018)

## 4.2.8 - 1/3/2024

#### APIs

* Fixed an issue where the API tester in the admin console wouldn't work in a nested IIS site (#3004)

#### Apps

* Fixed an issue where -Locale on New-UDDatePicker and New-UDTimePicker had no effect (#2988)
* Added Variables page to live documentation (#2991)
* Added -IgnoreResult to Invoke-UDJavaScript to work around a hang in certain circumstances (#2922)
* Fix issue with New-UDTextbox date hand enter (#3006)
* Fixed an issue with one of the examples for New-UDDataGrid
* Fixed an issue with one of the examples for New-UDForm (#2990)
* Added -DisableArcLinkLabels and -DisableArcLabels to New-UDNivoChart (#2907)

#### Automation

* Fixed an issue where the System Event page would show an error in the admin console (#2996)
* Fixed an issue where the job timer wouldn't display days (#3008)
* Fixed an issue where the admin console would display an error viewing a job (#2361)

#### Platform

* Fixed an issue where Azure DevOps git repositories could lose there tracking branch when clicking Synchronize Now
* Fixed a warning at startup about Computer Groups (#2989)
* Fixed an issue where the User Name computer tag would duplicate (#2997)
* Changed the default sort direction for Notifications (#3000)
* Fixed an issue with HTTPS certificate thumbprint lookups (#3002)
* Added support for custom computer tags (#2998)
* Fixed an issue where an extra new line character would be added to script scripts when splatting was enabled (#2995)
* Added the git repo link to the git commit page (#2956)
* Partial git commits now perform a git push (#2957)
* Fixed an issue where users could create app tokens for the system account (#3010)

## 4.2.7 - 12/18/2023

#### Apps

* Fixed an issue with -Schema parameter of New-UDForm's example in cmdlet help (#2896)
* Added Start Time and Deploy Time to app information (#2950)
* Added $AppRoot and $AppFullUrl variables (#2928)
* Fixed an issue where integrated apps didn't report memory usage (#2969)
* Value must be unique for New-UDTransferList (#2952)
* Fixed an issue where New-UDMap did not work with Get-UDElement (#2971)
* Fixed an issue where New-UDMap did not work with Add-UDElement (#2973)
* Fix issue with value on date type New-UDTextbox (#2961)
* Fixed an issue where where the PSU icon would not show up in in the app live docs in a nested IIS site (#2953)

#### Automation

* Fixed an issue where scheduled jobs run using schedules without a name would not behave properly when filtering scheduled jobs (#2955)
* Fixed an issue where rerunning jobs with date\time parameters would not populate correctly (#2944)
* Fixed an issue where Get-PSUJob -Id would not return the identity of the user that ran the script (#2945)
* Fixed an issue where the Job Completed trigger would not run on failed jobs (#2967)
* Fixed an issue concurrency issue that could occur when starting jobs using SQL persistence (#2964)

#### Platform

* Fixed an issue with SQL errors while grooming jobs with child jobs (#2894)
* Fixed an issue grooming idle terminals instances when the terminal was deleted (#2960)
* Added Delete All Notifications button (#2959)
* Fixed an issue where SQLite logging wouldn't work when using environment variables in the connection string (#2966)
* Added CertificateTypes configuration option for Certificate Authentication (#2985)

## 4.2.6 - 12/11/2023

#### APIs

* Fixed an issue where $Body was not available if param was specified (#2923)
* Fixed an issue where the Roles property didn't populate properly when editing an endpoint in the Admin Console (#2920)
* Fixed an issue where API Docs wouldn't handle basic types property for .INPUT and .OUTPUT (#2935)

#### Apps

* Fixed an issue where the live docs page logo wouldn't load properly in a nested site (#2919)
* Fixed an issue where the live docs page would not render properly when a user had many roles (#2919)
* Improved uncached client-side load time (#2926)
* Fixed an issue where apps memory would usage was miscalculated (#2941)
* Fixed an issue where pages would disappear if a PSU module with pages was installed (#2942)
* Fixed an issue where the PSU service could crash when attempting to serialize the results of Get-Service (#2940)
* Added support for custom app and page templates (#2927)

#### Automation

* Fixed an issue where the groom job could delete one time schedules before they ran (#2912)
* Removed Suspend from Error Action script property (#2924)

#### Platform

* Fixed an issue where not all cookies would be prefixed by the Kestrel \ CookiePrefix setting (#2846)
* Fixed an issue where git sync could lose its remote tracking branch
* Authentication and Role pages now use the log viewer (#2929)
* Log viewer defaults to text. Setting is now sticky (#2930)
* Fixed an issue where JWT, Cookies and Basic auth would not work against APIs when Windows Auth was enabled (#2254)
* Fixed an issue where PSEditorServices module was missing files
* Fixed an issue where adding Computer Groups wouldn't update in the Admin Console until refreshing the page (#2938)
* Fixed an issue where published folders would not work on Unix systems (#2947)
* Added View Repository and Status buttons on the git commit page (#2917)
* Verified PowerShell 7.4 support (#2860)

## 4.2.5 - 12/4/2023

**Known Issues**

* [KB0054 - Git Sync: There is no tracking information for the current branch](https://support.ironmansoftware.com/portal/en/kb/articles/git-sync-there-is-no-tracking-information-for-the-current-branch)
* [KB0055 - Blank Admin Console or No Updates After Upgrade](https://support.ironmansoftware.com/portal/en/kb/articles/kb0055-blank-admin-console-or-no-updates-after-upgrade)

#### APIs

* Fixed an issue where endpoint docs would not show the required tag on required parameters
* Fixed an issue where endpoint docs would not show array parameters properly
* Fixed an issue where Connect-PSUEventHub would not work in Windows PowerShell
* Fixed an issue with using basic authentication with endpoints

#### Apps

* Fixed an issue where Write-Progress wouldn't work properly with multiple connected clients (#2881)
* Fixed an issue where apps would not remain running on multi-node systems (#2854)
* Fixed an issue where New-UDUpload data would not be available in New-UDStepper (#2865)
* Fixed an issue where dashboards would not start if they had ps1 files in the pages folder that did not return New-UDPage
* Fixed an issue were the date filter type did not work in New-UDTable (#2898)
* Fixed an issue where New-UDDatePicker and New-UDTimePicker could not be cleared (#2892)
* Fixed an issue where New-UDDatePicker and New-UDTimePicker -TimeZone would have no effect. -TimeZone requires an IANA time zone ID. See https://mui.com/x/react-date-pickers/timezone/#supported-timezones for a list of valid time zones. (#2891)
* Fixed an issue with UDMap not rendering properly (#2535)
* Fixed an issue where New-UDSelect would fail when only a single item was present (#2916)

#### Automation

* Fixed an issue where certain views would not show scheduled jobs

#### Platform

* Fixed an issue where old git statuses would not be removed when resetting the git settings (#2884)
* Fixed an issue where /api/v1/cache/keys returned keys with a PSUCache prefix.
* Fixed an issue where logging targets would not honor the minimum level
* Disabled progressive web app for management console
* Fixed an issue where the -Minimal parameter couldn't be specified for environments in the Admin Console (#2908)
* Fixed an issue with the git commit file selector (#2877)
* Fixed an issue with published folders that started with a slash in the path (#2655)

## 4.2.4 - 11/24/2023

#### Apps

* Fixed an issue where Get-UDPage could return pages from the wrong app.

#### Automation

* Fixed an issue with the PowerShell serializer when saving schedules with splatting enabled (#2866)

#### Pages

* Fixed an issue with submitting forms on Pages

#### Platform

* Fixed an issue with Windows authentication in IIS when attempting to access the admin console.
* Fixed an issue where creating a new module in the admin console would return the error "Value Cannot Be Null (Parameter ‘s’)"
* Fixed an issue where using the certificate thumb print for a certificate with a subject that didn't start with "CN=" would fail to load the certificate.
* Fixed an issue where New-PSULoggingTarget could not be called remotely.

## 4.2.3 - 11/21/2023

#### Automation

* Fixed an issue where Get-PSUJob would not return scheduled jobs (#2867)

#### Apps

* Fixed an issue where nested files changes would not cause an autodeploy (#2863)

#### Platform

* Fixed an issue where Windows Auth logins would not work with the admin console

#### Desktop

* Fixed an issue where Desktop mode would not start properly.

#### Known Issues

* There is a known issue with Windows Auth and IIS that will be resolved in 4.2.4.&#x20;

## 4.2.2 - 11/20/2023

#### Apps

* Increased max websocket size to fix an issue with Get-UDElement failing on large objects like tables

#### Platform

* Fixed an issue where SAML2 logins would not work with the admin console (#2853)
* Added Kestrel:CookiePrefix setting to allow for multiple instances of PSU to run on the same server without sharing cookies (#2846)
* Fixed an issue where the git commit page would reload every second

## 4.2.1 - 11/16/2023

#### Critical

* Security Vulnerability Remote code execution in PowerShell Universal APIs (CVE-TBD) - [More Information](https://blog.ironmansoftware.com/powershell-universal-apis-cve/)

#### Apps

* Disabled service worker registration for apps to prevent caching of the index.html file (#2855)

## 4.2.0 - 11/14/2023

#### APIs

* Added -Local to Get-PSUEventHubConnection (#2715)
* Added support for calling Send-PSUEvent remotely (#2719)
* Improved API performance
* Added C# API plugin
* Added Set-PSUEndpoint
* Fixed an issue where renaming endpoint paths would not have any effect (#2737)

#### Apps

* Added -OnClick to New-UDCard (#2697)
* Removed the Mandatory flag for -Text on New-UDMenuItem (#2685)
* Fix style issue with -Multiple and -Icon on New-UDAutocomplete (#2632)
* Added -Variant to New-UDIconButton (#2363)
* Fixed styling issues with New-UDToggleButton (#2532)
* Get-UDPage -Name now works with Page names and file names (#2543)
* Added -CountDescription and -RowsPerPage to New-UDTableTextOption (#2219)
* Fixed name issues with New-UDSelectGroup (#2701)
* Improved performance of Get-UDElement (#2733)
* Apply -Dense to all sub-list items (#2749)
* Fixed an issue where New-UDDatePicker would return a string rather than a DateTime object (#2716)
* Make New-UDTransferList search case-insensitive (#2729)
* Added -FullHeight to Show-UDModal (#2722)
* Fixed an issue with Out-UDDataGridData where it would not filter properly
* Added -Dense, -LeftTitle, -LeftSubTitle, -RightTitle, -RightSubTitle to New-UDTransferList (#2714)
* Improved App Designer properties layout (#2793)
* Automatic navigation now uses -Title as the link for the navigation link (#2758)
* Improved the performance of New-UDDataGrid checkbox selection
* Added -Wait to Sync-UDElement
* Added -Sx to New-UDSelect
* Fix issue with single char issue on New-UDTextbox (#2800)
* Fix variant when using -Mask on New-UDTextbox (#2807)
* Added app page properties (#2757/#2567)
* Added -Icon to New-UDButtonGroupItem (#2789)
* Added -Color, -Disabled, -FullWidth, -Orientation, -Size, -Sx, and -Variant to New-UDButtonGroup (#2789)
* Added live docs for New-UDButtonGroup (#2789)
* Fixed an issue with New-UDDataGridColumn default values (#2828)
* Fixed an issue where using the logout button would not forward back to the app after logging in again (#2642)
* Added -OnRowStyle and -HeaderStyle to New-UDTable (#156, #758)
* Fixed an issue where Sync-UDElement could throw an exception
* Added -IdentityColumn, -RowHeight, -HideExport and -DisableRowSelectionOnClick to New-UDDataGrid
* Fixed card margin issue (#2801)
* Fixed issue with -ShowLoading with dark themes (#2691)

#### Automation

* Added a filter for job status (#2694)
* Added support for minimal job environments
* Added support for hiding scheduled jobs (#2710)
* Fixed an issue with Invoke-PSUScript and SecureString parameters
* Wait-PSUJob now supports -JobId
* Wait-PSUJob now returns pipeline output and terminating errors
* Invoke-PSUScript now supports -WaitTimeout
* Added -Schedule to Get-PSUJob
* Fixed an issue starting terminals in the Agent environment
* Added -Parameters to New-PSUSchedule and updated the serializer to use this format by default
* Fixed an issue where Get-PSUSchedule -Integrated would not return the NextExecutionTime
* Added -Parameters to Invoke-PSUScript

#### Platform

* Added New-PSUHealthCheck and New-PSUHealthCheckResult (#2522)
* Added Conflict Module Health check (#2700)
* Adjusted the authentication re-check on the login page to reduce 401s (#2688)
* Dashboard and API endpoint files are now deleted when the resource is removed. (#2676)
* Added the ability to configure disabled drives for the Drive Space health check (#2476)
* Fixed an issue with overlapping tooltips on the computer delete button (#2707)
* Added reserve proxy plugin (YARP)
* Added OpenTelemetry plugin
* Added reload configuration file dropdown
* Added a minimap toggle to the editor
* Fixed an issue with loading Az.Accounts in PSU
* Updated Swashbuckle NuGet package (##2682)
* Included PSResourceGet GA module and remove pre-release PSGet (#2740)
* PowerShell Universal can now be installed as a Progressive Web App
* Added static PowerShell 7 environment to prevent issues when upgrading the underlying PowerShell version (#2765)
* Fixed an issue with array variables (#2693)
* Fixed an issue where the agent environment wouldn't work on Linux
* Added support for Computer Groups and accompanying cmdlets
* Added -FileEncoding to Set-PSUSetting
* Added Basic authentication
* Added Get-PSUGitSetting, Set-PSUGitSetting and Remove-PSUGitSetting
* Added Merge-PSUGitEdit, Start-PSUGitEdit and Stop-PSUGitEdit
* Added Sync-PSUGit
* Added -Commits, -UncommittedChanges, -EditInProgress to Get-PSUGitStatus
* Fixed an issue with -DefaultRoute on New-PSURole not working with forms authentication
* Modified variable properties (#2778)
* Added Clear-PSUCache

#### Deprecated

* Queues configured in appsettings.json - Replaced with computer groups
* Browser based debugging tools - Replaced with VS Code extension

## 4.1.10 - 11/16/2023

#### Critical

* Security Vulnerability Remote code execution in PowerShell Universal APIs (CVE-TBD)

## 4.1.8 - 10/30/2023

#### Apps

* Fixed an issue where clicking off the Read-Host dialog would not be treated as a cancel
* Fixed an issue where clicking cancel in PromptForChoice would result in an exception (#2806)
* Fix issue with single char issue on New-UDTextbox (#2800)
* Added $ENV:PSU\_APP\_PAGE\_MAX to allow for customizing the max number of page (tab) states are stored in memory per session, per dashboard.

#### Automation

* Fixed an issue where Invoke-PSUScript could throw an exception when -Wait is specified in a non-integrated environment while using SQL persistence

#### Platform

* Added -File to Sync-PSUConfiguration

## 4.1.7 - 10/23/2023

#### Apps

* Fixed an issue where Read-Host Cancel would return an error when clicking the cancel button (#2769)
* Fixed an issue where dashboards would fail to start or stop with a 500 error
* Fixed an issue with variable scoping in rendered table rows (#2776)
* Fixed an issue where New-UDAutocomplete -Value wouldn't work when -Multiple was specified (#2698)
* Fixed an issue where certain formats of $EventData would return a DateTime rather than the expected string

#### Automation

* Fixed an issue where credential variables with roles could throw an exception when starting a job (#2762)
* Fixed an issue where Invoke-PSUScript -Wait would throw an error (#2777)

#### Platform

* Fixed an issue where the secret provider did not honor environment variables (#2753)
* Fixed an issue where logging for roles was not displaying properly (#2766)
* SystemLogLevel now defaults to Information
* Added error handling around PSScriptAnalyzer formatting
* Enabled gRPC logging
* Fixed a file locking issue with configuration files

## 4.1.6 - 10/16/2023

#### APIs

* Fixed an issue where the $Data variable was not populated.

#### Apps

* Fixed an issue where Windows authentication would display as anonymous in User Sessions for apps.
* Fixed an issue where Sync-UDElement + New-UDElement cause event handlers to fail. (#2747)
* Fixed an issue where New-UDDatePicker would return the current day rather than $null when no date was selected. (#2734)
* Fixed an issue where New-UDDatePicker would return a string rather than a DateTime object (#2716)
* Fixed vertical alignment of New-UDAlert -Dense (#2724)
* Fixed an issue where Read-Host would return the previous value if Cancel was clicked the second time
* Fixed an issue where Ok and Cancel would both return an empty string from Read-Host. Now cancel returns $null and Ok returns an empty string.
* Make New-UDTransferList search case-insensitive (#2729)
* $Query is now case-insensitive (#2752)
* Fixed an issue where -Variant fullWidth didn't work on New-UDTabs
* Add a delete pages button and tab to the admin console (#2755)

#### Automation

* Fixed an issue where Get-PSUJob -Id-RunId would behave differently depending on where you were running it (#2750)

#### Platform

* Adjusted the admin console build to avoid inline JavaScript
* Removed Policy Defined from the App Token Role selector since it is not a valid value for tokens (#2739)
* Fixed an issue where updating git settings would clear out the username and password (#2742)

## 4.1.5 - 10/9/2023

#### APIs

* Improved API performance

#### Apps

* Push -Dense down to children on New-UDList (#2677)

#### Platform

* Fixed a concurrency issue during authentication when using SQL persistence that could result in SQL exceptions
* Fixed an issue where SQLite persistence would create an errant file and folder in the repository directory
* Fixed an issue where SQLite persistence did not properly support environment variables.
* Remote access is now supported for developer licenses.

## 4.1.4 - 10/2/2023

#### Platform

* Rolling back a change made to support Az.Accounts in the integrated environment as it was causing problems with OIDC and JWT authentication (#2718)

## 4.1.3 - 10/2/2023

#### Automation

* Fixed an issue where viewing script properties with tags assigned would show a JavaScript error.
* Fixed an issue where the rerun job button wasn't present for jobs with a warning status (#2708)
* Fixed an issue where scripts edited in the admin console wouldn't reload parameters
* Fixed an issue where retrying jobs wouldn't work when using SQL persistence (#2706)
* Fixed an issue where parameter sets would not be available in the create schedule dialog (#2712)

#### Apps

* Fixed an issue where the View Code button would not work in the App Designer.
* Fixed an issue where extra lines were added to event handlers in the App Designer.

#### Platform

* Fixed an issue where the ModuleRefreshInterval setting would not work after a restart of the service.
* Fixed an issue where Az.Accounts could not be loaded into the integrated environment (#2681)

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
