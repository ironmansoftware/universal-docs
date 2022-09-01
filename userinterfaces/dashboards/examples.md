---
description: Examples of things you can do with dashboards.
---

# Examples

## Stopwatch

This example shows how to create a stopwatch component in PowerShell Universal Dashboard.

```powershell
New-UDDashboard -Title 'Stopwatch' -Content {
    New-UDDynamic -Id 'stopwatch' -Content {
        (Get-Date).ToString('T')
    } -AutoRefresh -AutoRefreshInterval 1
    
    New-UDButton -Text 'Toggle Stopwatch' -OnClick {
        Set-UDElement -Id 'stopwatch' -Properties @{
            autoRefresh = -not( (Get-UDElement -Id 'stopwatch').AutoRefresh)
        }
    }
}
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
