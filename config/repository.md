---
description: Information about the PowerShell Universal repository.
---

# Repository

The configuration data for PowerShell Universal is primarily stored within the repository. By default, the repository folder can be found in `%ProgramData%\UniversalAutomation\Repository`. You can adjust the location of the repository by editing the `appsettings.json` file.&#x20;

The repository contains PowerShell scripts and XML files that are produced when using the PowerShell Universal admin console. The repository folder is also watched for changes so any change made on disk will cause the system to reload the file and reconfigure the platform. When using Git integration, the repository folder is what is synchronized with the git remote.&#x20;

All configuration cmdlets are part of the [Universal ](https://www.powershellgallery.com/packages/Universal)module.

## What's Stored in the Repository

Files stored in the repository are stored as plain text to allow for easy differencing with source control tools.&#x20;

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

These entities are stored within the PowerShell Universal database.&#x20;

* App Tokens
* Identities
* Job History

## Editing the Repository

You can edit the repository files directly in the admin console by navigating to Settings \ Configurations. The editor allows you to create files and folders and edit any file within the repository directory.&#x20;

![](<../.gitbook/assets/image (341).png>)

## Configuration Scripts

### Authentication.ps1

{% hint style="info" %}
Stored in `.universal\authentication.ps1`
{% endhint %}

This script is responsible for configuring f[orms authentication](security/#forms-authentication). If forms authentication is not being used, this file is ignored.&#x20;

You can use the [`Set-PSUAuthentication` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Set-PSUAuthenticationMethod.txt)cmdlet in this file.&#x20;

### Dashboards.ps1

{% hint style="info" %}
Stored in `.universal\dashboards.ps1`
{% endhint %}

This script is responsible for registering PS1 files are [dashboards ](../userinterfaces/dashboards/)with the system. Each command contains the meta-data for the dashboard including name, base URL, and environment.&#x20;

You can use the [`New-PSUDashboard` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUDashboard.txt)cmdlet in this file.&#x20;

### Endpoints.ps1

{% hint style="info" %}
Stored in `.universal\endpoints.ps1`
{% endhint %}

This script is responsible for defining all the [API endpoints](api.md) within the PowerShell Universal instance.&#x20;

You can use the [`New-PSUEndpoint` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUEndpoint.txt)cmdlet in this file.&#x20;

### Environments.ps1

{% hint style="info" %}
Stored in `.universal\environments.ps1`
{% endhint %}

This script is responsible for defining all the environments within PowerShell Universal.&#x20;

You can use the [`New-PSUEnvironment` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUEnvironment.txt)cmdlet in this file.&#x20;

### Licenses.ps1

{% hint style="info" %}
Stored in `.universal\licenses.ps1`
{% endhint %}

This script is responsible for defining the license used in PowerShell Universal.

You can use the [`Set-PSULicense` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Set-PSULicense.txt)cmdlet in this file.

```
Set-PSULicense -Key "<License></License>"
```

### LoginPage.ps1

{% hint style="info" %}
Stored in `.universal\loginPage.ps1`
{% endhint %}

This script is responsible for configuring a custom [login page](login-page.md).&#x20;

You can use the [`New-PSULoginpage`](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSULoginPage.txt) and [`New-PSULoginPageLink` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSULoginPageLink.txt)in this file.&#x20;

### Init.ps1

{% hint style="info" %}
Stored in `.universal\init.ps1`
{% endhint %}

This script runs before any configuration is done within PowerShell Universal. The server is running but none of the services have started. This is useful for install modules or configuring secret vaults before discovery of those resources are started.&#x20;

### Pages

{% hint style="info" %}
Stored in the `pages` folder.
{% endhint %}

This folder contains the page XML files. These are not intended to be edited manually and should be edited with the page designer.&#x20;

### PublishedFolders.ps1

{% hint style="info" %}
Stored in `.universal\publishedFolders.ps1`
{% endhint %}

This script is responsible for configuring [published folders](../platform/published-folders.md).

You can use the [`New-PSUPublishedFolder` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUPublishedFolder.txt)cmdlet in this file.&#x20;

### RateLimits.ps1

{% hint style="info" %}
Stored in `.universal\rateLimits.ps1`
{% endhint %}

This script is responsible for configuring [rate limits](../api/rate-limiting.md).&#x20;

You can use the [`New-PSURateLimit` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSURateLimit.txt)cmdlet in this file.&#x20;

### Roles.ps1

{% hint style="info" %}
Stored in `.universal\roles.ps1`
{% endhint %}

This script is responsible for configuring [roles](../userinterfaces/dashboards/role-based-access.md).

You can use the [`New-PSURole` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSURole.txt)cmdlet in this file.&#x20;

### Schedules.ps1

{% hint style="info" %}
Stored in `.universal\schedules.ps1`
{% endhint %}

This script is responsible for configuring [schedules](../automation/schedules.md).

You can use the [`New-PSUSchedule` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUSchedule.txt)cmdlet in this file.&#x20;

### Scripts.ps1

{% hint style="info" %}
Stored in `.universal\scripts.ps1`
{% endhint %}

This script contains the meta-data for [scripts](../automation/scripts/). Actual scripts can be stored anywhere. The path that is included is relative to the repository. Full path names are also allowed.&#x20;

You can use the [`New-PSUScript` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUScript.txt)cmdlet in this file.&#x20;

### Settings.ps1

{% hint style="info" %}
Stored in `.universal\settings.ps1`
{% endhint %}

This script is responsible for configuring system [settings](settings.md).&#x20;

You can use the [`Set-PSUSetting` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Set-PSUSetting.txt)cmdlet in this file.&#x20;

### Tags.ps1

{% hint style="info" %}
Stored in `.universal\tags.ps1`
{% endhint %}

This script is responsible for configuring tags.&#x20;

You can use the [`New-PSUTag` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUTag.txt)cmdlet in this file.&#x20;

### Triggers.ps1

{% hint style="info" %}
Stored in `.universal\triggers.ps1`
{% endhint %}

This script is responsible for configuring [triggers](../automation/triggers.md).

You can use the [`New-PSUTrigger` ](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUTrigger.txt)cmdlet in this file.&#x20;

### Variables&#x20;

{% hint style="info" %}
Stored in `.universal\variables.ps1`
{% endhint %}

This script is responsible for configuring [variables](../userinterfaces/pages/variables.md).

You can use the [`New-PSUVariable`](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUVariable.txt) cmdlet in this file.

## Custom Configuration Script

A custom configuration script can be executed within the configuration process. The path to the configuration script can be defined in `appsettings.json` or as an environment variable.&#x20;

{% code title="appsettings.json" %}
```json
"Data": {
    "ConfigurationScript": "customScript.ps1"
}
```
{% endcode %}

{% code title="Environment Variable" %}
```powershell
$Env:Data__ConfigurationScript = "customScript.ps1"
```
{% endcode %}

You can chose to return items such as endpoints, scripts or dashboards from the script. Additionally, you can use this script to configure resources like modules and secret vaults before the system is started.&#x20;
