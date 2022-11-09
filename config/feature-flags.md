---
description: Disable features within PowerShell Universal.
---

# Feature Flags

Using feature flags, you can disable features that you don't use to simplify your deployments. This can be useful to make the platform easier to use and reduce attack vectors from a security standpoint.&#x20;

## Disable Features

To disable built-in features, you can use the `-DisabledFeatures` parameter of `Set-PSUSetting`.

```powershell
$Parameters = @{
    DisabledFeatures = ([PowerShellUniversal.Features]::Api -bor [PowerShellUniversal.Features]::Pages)
}
Set-PSUSetting @Parameters
```

Once a feature has been disabled, it will no longer appear in the admin console.&#x20;

![](../.gitbook/assets/image.png)

More importantly, disabled features will be completely disabled in the PowerShell Universal server. The Management APIs will no longer function, and the configuration scripts will not be run.&#x20;

Features that can be disabled include:&#x20;

* API
* Scripts
* Terminals
* Dashboards
* Pages
* RateLimiting
* PublishedFolders
* Templates
* Protect

## Experimental Features

Experimental features are disabled by default. To enable an experiment feature, use the `-ExperimentalFeatures` parameter of `Set-PSUSetting`.&#x20;

```powershell
$Parameters = @{
	ExperimentalFeatures = ([PowerShellUniversal.ExperimentalFeatures]::CSharpLang)
}
Set-PSUSetting @Parameters 
```

Experimental features may not have a user interface component when enabled.&#x20;
