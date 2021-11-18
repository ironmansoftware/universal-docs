---
description: Dynamic regions allow you control the reload of data within the region.
---

# Dynamic Regions

`New-UDDynamic` allows you to define a dynamic region. Pages themselves are dynamic in nature. This means that every time a page is loaded, it runs the PowerShell for that page. Sometimes, you may want to reload a section of a page rather than the whole page itself. This is when you will want to use dynamic regions.

## Basic Dynamic Region

This dynamic region reloads when the button is clicked.

```powershell
New-UDDashboard -Title "Hello, World!" -Content {
    New-UDDynamic -Id 'date' -Content {
        New-UDTypography -Text "$(Get-Date)"
    }

    New-UDButton -Text 'Reload Date' -OnClick { Sync-UDElement -Id 'date' }
}
```

![Reload on button click](../../../.gitbook/assets/nzjtyyol54.gif)

## Auto Refresh

Dynamic regions enable the ability to auto refresh components after a certain amount of time. The entire region's script block will be run when autorefreshing.

{% hint style="info" %}
If you have multiple related components that use the same data, consider putting them in the same dynamic region to improve performance.
{% endhint %}

```powershell
    New-UDDynamic -Id 'date' -Content {
        New-UDTypography -Text "$(Get-Date)" -Variant h3
        New-UDTypography -Text "$(Get-Random)" -Variant h3
    } -AutoRefresh -AutoRefreshInterval 1
```

![Auto refresh dynamic region](../../../.gitbook/assets/jfrntplfw0.gif)

## Loading Component

Sometimes refreshing a dynamic component may take some time. For example, if you are querying another service's REST API or a data. Dynamic regions support configuration of the component that shows when the region is reloading. By default, nothing is shown. This can be any Universal Dashboard component.

```powershell
    New-UDDynamic -Content {
        Start-Sleep -Seconds 3
        New-UDTypography -Text "Done!"
    } -LoadingComponent {
        New-UDProgress -Circular
    }
```

![Loading component for dynamic region](../../../.gitbook/assets/vwly75oka9.gif)

## API

[New-UDDynamic](../../../cmdlets/New-UDDynamic.txt)
