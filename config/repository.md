---
description: Information about the PowerShell Universal repository.
---

# Repository

The configuration data for PowerShell Universal is primarily stored within the repository. By default, the repository folder can be found in `%ProgramData%\UniversalAutomation\Repository`. You can adjust the location of the repository by editing the `appsettings.json` file.

The repository contains PowerShell scripts and XML files that are produced when using the PowerShell Universal admin console. The repository folder is also watched for changes so any change made on disk will cause the system to reload the file and reconfigure the platform. When using Git integration, the repository folder is what is synchronized with the git remote.

All configuration cmdlets are part of the [Universal ](https://www.powershellgallery.com/packages/Universal)module.

## What's Stored in the Repository

Files stored in the repository are stored as plain text to allow for easy differencing with source control tools.

* Authentication
* Apps
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
* Vaults

## What's Not Stored in the Repository

These entities are stored within the PowerShell Universal database.

* App Tokens
* Identities
* Job History

## Editing the Repository

You can edit the repository files directly in the admin console by navigating to Settings \ Files. The editor allows you to create files and folders and edit any file within the repository directory.

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

You can also edit the repository directly on disk using editors like Visual Studio Code. By default, files are stored in `%ProgramData%\UniversalAutomation\Repository`. You will need to toggle the node into VS Code editing mode. The toggle to do so can be found on the home page. Only administrators will see this button and, if Disable Code First Editing is on in Settings \ General, you will not be able to change the edit mode.&#x20;

<figure><img src="../.gitbook/assets/image (296).png" alt=""><figcaption></figcaption></figure>

## Configuration Scripts

### Authentication.ps1

{% hint style="info" %}
Stored in `.universal\authentication.ps1`
{% endhint %}

This script is responsible for configuring [forms authentication](security/#forms-authentication). If forms authentication is not being used, this file is ignored.

You can use the [`Set-PSUAuthentication` ](../cmdlets/Set-PSUAuthenticationMethod.txt)cmdlet in this file.

### Branding.ps1

{% hint style="info" %}
Stored in `.universal\branding.ps1`
{% endhint %}

This script is responsible for configuring branding settings.

You can use the New-PSUBranding cmdlet in this file.

### Dashboards.ps1

{% hint style="info" %}
Stored in `.universal\dashboards.ps1`
{% endhint %}

This script is responsible for registering PS1 files are apps within the system. Each command contains the meta-data for the app including name, base URL, and environment.

You can use the [`New-PSUApp` ](../cmdlets/New-PSUDashboard.txt)cmdlet in this file.

### Endpoints.ps1

{% hint style="info" %}
Stored in `.universal\endpoints.ps1`
{% endhint %}

This script is responsible for defining all the [API endpoints](broken-reference/) within the PowerShell Universal instance.

You can use the [`New-PSUEndpoint` ](../cmdlets/New-PSUEndpoint.txt)cmdlet in this file.

### Environments.ps1

{% hint style="info" %}
Stored in `.universal\environments.ps1`
{% endhint %}

This script is responsible for defining all the environments within PowerShell Universal.

You can use the [`New-PSUEnvironment` ](../cmdlets/New-PSUEnvironment.txt)cmdlet in this file.

### healthChecks.ps1

{% hint style="info" %}
Stored in `.universal\healthChecks.ps1`
{% endhint %}

This script is responsible for defining Health Checks within PowerShell Universal.

You can use the [`New-PSUHealthCheck` ](../cmdlets/New-PSUHealthCheck.txt)cmdlet in this file.

### Licenses.ps1

{% hint style="info" %}
Stored in `.universal\licenses.ps1`
{% endhint %}

This script is responsible for defining the license used in PowerShell Universal.

You can use the [`Set-PSULicense` ](../cmdlets/Set-PSULicense.txt)cmdlet in this file.

```
Set-PSULicense -Key "<License></License>"
```

### Initialize.ps1

{% hint style="info" %}
Stored in `.universal\initialize.ps1`
{% endhint %}

This script runs before any configuration is done within PowerShell Universal. The server is running but none of the services have started. This is useful for install modules or configuring secret vaults before discovery of those resources are started.

### Middleware.ps1

{% hint style="info" %}
Stored in `.universal\middleware.ps1`
{% endhint %}

Allows for customization of the HTTP requests in PowerShell Universal.

### PublishedFolders.ps1

{% hint style="info" %}
Stored in `.universal\publishedFolders.ps1`
{% endhint %}

This script is responsible for configuring [published folders](../platform/published-folders.md).

You can use the [`New-PSUPublishedFolder` ](../cmdlets/New-PSUPublishedFolder.txt)cmdlet in this file.

### RateLimits.ps1

{% hint style="info" %}
Stored in `.universal\rateLimits.ps1`
{% endhint %}

This script is responsible for configuring [rate limits](../api/rate-limiting.md).

You can use the [`New-PSURateLimit` ](../cmdlets/New-PSURateLimit.txt)cmdlet in this file.

### Roles.ps1

{% hint style="info" %}
Stored in `.universal\roles.ps1`
{% endhint %}

This script is responsible for configuring [roles](../apps/role-based-access.md).

You can use the [`New-PSURole` ](../cmdlets/New-PSURole.txt)cmdlet in this file.

### Schedules.ps1

{% hint style="info" %}
Stored in `.universal\schedules.ps1`
{% endhint %}

This script is responsible for configuring [schedules](../automation/schedules.md).

You can use the [`New-PSUSchedule` ](../cmdlets/New-PSUSchedule.txt)cmdlet in this file.

### Scripts.ps1

{% hint style="info" %}
Stored in `.universal\scripts.ps1`
{% endhint %}

This script contains the meta-data for [scripts](../automation/scripts/). Actual scripts can be stored anywhere. The path that is included is relative to the repository. Full path names are also allowed.

You can use the [`New-PSUScript` ](../cmdlets/New-PSUScript.txt)cmdlet in this file.

### Settings.ps1

{% hint style="info" %}
Stored in `.universal\settings.ps1`
{% endhint %}

This script is responsible for configuring system [settings](settings.md).

You can use the [`Set-PSUSetting` ](../cmdlets/Set-PSUSetting.txt)cmdlet in this file.

### Tags.ps1

{% hint style="info" %}
Stored in `.universal\tags.ps1`
{% endhint %}

This script is responsible for configuring tags.

You can use the [`New-PSUTag` ](../cmdlets/New-PSUTag.txt)cmdlet in this file.

### Triggers.ps1

{% hint style="info" %}
Stored in `.universal\triggers.ps1`
{% endhint %}

This script is responsible for configuring [triggers](../automation/triggers.md).

You can use the [`New-PSUTrigger` ](../cmdlets/New-PSUTrigger.txt)cmdlet in this file.

### Variables.ps1

{% hint style="info" %}
Stored in `.universal\variables.ps1`
{% endhint %}

This script is responsible for configuring [variables](broken-reference/).

You can use the [`New-PSUVariable`](../cmdlets/New-PSUVariable.txt) cmdlet in this file.

### Vaults.ps1

{% hint style="info" %}
Stored in `.universal\vaults.ps1`
{% endhint %}

This script is responsible for configuring [vaults](../platform/variables.md#vaults).

## Templates

Using the Templates folder within the Repository, you can create a selection of item templates for commonly used features in PowerShell Universal. This includes apps, app pages, scripts and endpoints.

<figure><img src="../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption><p>Script Template</p></figcaption></figure>

PS1 files in the following folders will be provided as templates in the admin console.

* Templates \ App
* Templates \ AppPage
* Templates \ Endpoint
* Templates \ Script

## .psuignore

The `.psuignore`file can be used to exclude certain files or patterns from the file system watcher in PowerShell Universal. This is useful when saving files like logs to the repository directory. The format of the file should be a single regular expression per line. If the regular expression matches a path, the configuration system will ignore it.

```
logs.*
.git.*
```

## Read-Only Configuration Sections

Read-Only sections allow you to include script in your configuration files that will not be touched by changes in the admin console. This allows you to run additional logic, generate resources dynamically and create classes for use in OpenAPI schemas.

The `PSUHeader` region is placed at the top of your script. `PSUFooter` is placed at the bottom.

```powershell
#region PSUHeader 

1..100 | ForEach-Object {
    New-PSUEndpoint -Url "/endpoint/$_" -Endpoint {

    }
}

#endregion

New-PSUEndpoint -Url "/user" -Endpoint {

}

#region PSUFooter
#endregion
```

## Database Resources

You can optionally configure resources to be stored in the database rather than within the configuration repository. These resources will no longer be stored on disk and will be stored directly in the database. This makes them instantly available to allow connected computers in the PSU cluster.&#x20;

{% hint style="warning" %}
When configured, configuration files for resources will be ignored.
{% endhint %}

Some resources are not supported. These include:

* Apps
* Endpoints with paths
* Scripts
* Modules

To configure a resource for database persistence, you need to setup the [App Settings](settings.md) for each class type. Below is an example of storing schedules within the database.

```json
{
    "Data": {
        "Persistence" : {
            "Schedule": "Database",
            "ScheduleParameter": "Database"
        }
    }
}
```
