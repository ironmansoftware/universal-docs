---
description: Dynamic component for Blazor apps.
---

# Dynamic

The dynamic component allows you to run PowerShell script to generate PSBlazor components on the fly. It's context aware.&#x20;

{% hint style="warning" %}
Because dynamic components run PowerShell with each render, they can reduce the performance of your apps.&#x20;
{% endhint %}

A dynamic component is defined with a function that will be executed when the app is loaded.&#x20;

```xml
<Dynamic Function="RenderMyDynamic" />
```

Within the dynamic, return a string that will be rendered. It must be valid PSBlazor syntax.&#x20;

```powershell
function RenderMyDynamic {
    "<Alert Message='Cool!' />"
}
```

If you are using a dynamic within a component that sets a context variable, you can use the context in your function. In this example, we have a table of services that uses a dynamic in the status column.

```markup
<Table DataSource="$Services">
    <PropertyColumn Property="Name" />
    <PropertyColumn Property="Status">
        <Dynamic Function="RenderStatusColumn" />
    </PropertyColumn>
</Table>
```

The function `RenderStatusColumn` will be called for each row in the table.&#x20;

```powershell
function RenderStatusColumn {
    param($Context)
    
    if ($Context.Status -eq 'Started')
    {
        "<Alert Message='Running' />"
    }
    else 
    {
        "<Alert Message='$($Context.Status)' />"
    }
}
```
