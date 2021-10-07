---
description: Information about the PowerShell Universal repository.
---

# Repository

The configuration data for PowerShell Universal is primarily stored within the repository. By default, the repository folder can be found in `%ProgramData%\UniversalAutomation\Repository`. You can adjust the location of the repository by editing the `appsettings.json` file. 

The repository contains PowerShell scripts and XML files that are produced when using the PowerShell Universal admin console. The repository folder is also watched for changes so any change made on disk will cause the system to reload the file and reconfigure the platform. When using Git integration, the repository folder is what is synchronized with the git remote. 

All configuration cmdlets are part of the [Universal ](https://www.powershellgallery.com/packages/Universal)module.

## What's Stored in the Repository

* Authentication
* Dashboards
* Endpoints
* Environments
* Licenses
* Login Pages
* Pages
* Published Folders
* Rate Limits
* Roles
* Schedules
* Scripts
* Settings
* Tags
* Triggers

## What's Not Stored in the Repository

* App Tokens
* Identities
* Job History

## Configuration Scripts

### Authentication.ps1

{% hint style="info" %}
Stored in `.universal\authentication.ps1`
{% endhint %}

This script is responsible for configuring f[orms authentication](security/#forms-authentication). If forms authentication is not being used, this file is ignored. 

You can use the `Set-PSUAuthentication` cmdlet in this file. 

### Dashboards.ps1

{% hint style="info" %}
Stored in `.universal\dashboards.ps1`
{% endhint %}

This script is responsible for registering PS1 files are [dashboards ](../userinterfaces/dashboards/)with the system. Each command contains the meta-data for the dashboard including name, base URL, and environment. 

You can use the `New-PSUDashboard` cmdlet in this file. 

### Endpoints.ps1

{% hint style="info" %}
Stored in `.universal\endpoints.ps1`
{% endhint %}

This script is responsible for defining all the [API endpoints](api.md) within the PowerShell Universal instance. 

You can use the `New-PSUEndpoint` cmdlet in this file. 

### Environments.ps1

{% hint style="info" %}
Stored in `.universal\environments.ps1`
{% endhint %}

This script is responsible for defining all the environments within PowerShell Universal. 

You can use the `New-PSUEnvironment` cmdlet in this file. 

### Licenses.ps1

{% hint style="info" %}
Stored in `.universal\licenses.ps1`
{% endhint %}

This script is responsible for defining the license used in PowerShell Universal.

You can use the `Set-PSULicense` cmdlet in this file.

### LoginPage.ps1

{% hint style="info" %}
Stored in `.universal\loginPage.ps1`
{% endhint %}

This script is responsible for configuring a custom [login page](login-page.md). 

You can use the `New-PSULoginpage` and `New-PSULoginPageLink` in this file. 

### Pages

{% hint style="info" %}
Stored in the `pages` folder.
{% endhint %}

This folder contains the page XML files. These are not intended to be edited manually and should be edited with the page designer. 

### PublishedFolders.ps1

{% hint style="info" %}
Stored in `.universal\publishedFolders.ps1`
{% endhint %}

This script is responsible for configuring [published folders](../platform/published-folders.md).

You can use the `New-PSUPublishedFolder` cmdlet in this file. 

### RateLimits.ps1

{% hint style="info" %}
Stored in `.universal\rateLimits.ps1`
{% endhint %}

This script is responsible for configuring [rate limits](../api/rate-limiting.md). 

You can use the `New-PSURateLimit` cmdlet in this file. 

### Roles.ps1

{% hint style="info" %}
Stored in `.universal\roles.ps1`
{% endhint %}

This script is responsible for configuring [roles](../userinterfaces/dashboards/role-based-access.md).

You can use the `New-PSURole` cmdlet in this file. 

### Schedules.ps1

{% hint style="info" %}
Stored in `.universal\schedules.ps1`
{% endhint %}

This script is responsible for configuring [schedules](../automation/schedules.md).

You can use the `New-PSUSchedule` cmdlet in this file. 

### Scripts.ps1

{% hint style="info" %}
Stored in `.universal\scripts.ps1`
{% endhint %}

This script contains the meta-data for [scripts](../automation/scripts/). Actual scripts can be stored anywhere. The path that is included is relative to the repository. Full path names are also allowed. 

You can use the `New-PSUScript` cmdlet in this file. 

### Settings.ps1

{% hint style="info" %}
Stored in `.universal\settings.ps1`
{% endhint %}

This script is responsible for configuring system [settings](settings.md). 

You can use the `Set-PSUSetting` cmdlet in this file. 

### Tags.ps1

{% hint style="info" %}
Stored in `.universal\tags.ps1`
{% endhint %}

This script is responsible for configuring tags. 

You can use the `New-PSUTag` cmdlet in this file. 

### Triggers.ps1

{% hint style="info" %}
Stored in `.universal\triggers.ps1`
{% endhint %}

This script is responsible for configuring [triggers](../automation/triggers.md).

You can use the `New-PSUTrigger` cmdlet in this file. 

