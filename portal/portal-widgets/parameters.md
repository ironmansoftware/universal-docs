---
description: Parameters for Portal Widgets.
---

# Parameters

You can define the `Initialize-PSUWidget` function to add parameters to Widgets. Parameters are displayed as properties in both the widget editor and page designer.&#x20;

## Initialize-PSUWidget

Define a function named `Initialize-PSUWidget` to accept parameters and define initialization logic for when the widget is shown.&#x20;

```powershell
function Initialize-PSUWidget {
    param(
        [Parameter()]
        $Param1
    )
    
    if ($Param1 -eq 'Script')
    {
       $Variables["Type"] = "Script"
    }
}
```
