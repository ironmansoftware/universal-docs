---
description: Plugins that extend the PowerShell Universal platform.
---

# Plugins

Plugins are functionality that are not enabled by default. A publicly available plugin API is currently being developed and will be released with a future version of PowerShell Universal. Below are a list of the plugins that are shipped with PowerShell Universal v4.2 and later.

## Enabling Plugins

Plugins are enabled in `appsettings.json` or through environment variables. See [App Settings ](../../config/settings.md)for information on where to configure these options. Any changes made to the configuration will require a restart of the PowerShell Universal service.

```json
{
    "Plugins": [
        "SQL",
        "PowerShellUniversal.Language.CSharp"
    }
}
```

##
