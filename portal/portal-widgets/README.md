---
description: Information about creating portal widgets.
---

# Portal Widgets

Widgets are user interfaces blocks built with PowerShell and Blazor. You can create robust web-based used interfaces with minimal web development experience.

## Built In Widgets

PowerShell Universal offers built in widgets to integrate with other features in the platform to display UI elements.&#x20;

### Script Form

Provide a form to end users to run scripts. The selected script will need a role defined under the Portal tab in the script's properties. If the script is not available to the user based on role, they will no be able to see the form.&#x20;

### Script Table

<figure><img src="../../.gitbook/assets/image (257).png" alt=""><figcaption><p>Script Table</p></figcaption></figure>

The script table widget will display a table based on the last output of a script. This selects the most recent job and generates the table based on the properties of the objects returned. For example, try running a script that returns processes on the current machine.&#x20;

```powershell
Get-Process | Select-Object Name, Id
```

### Script Pie Chart

<figure><img src="../../.gitbook/assets/image (253).png" alt=""><figcaption><p>Script Pie Chart</p></figcaption></figure>

The script pie chart widget displays a chart based on data from the last run of a script. The script needs to output data in a particular format in order to define the chart's slices. Below is an example of how to generate data for a pie chart.

```powershell
1..5 | ForEach-Object {
    [PSCustomObject]@{ 
        type = "Category $_"
        value = Get-Random -Min 5 -Max 60
    }
}
```

In the properties for the pie chart widget, set the Category Property to `type` and the Value Property `value`.

### Script Line Chart

<figure><img src="../../.gitbook/assets/image (252).png" alt=""><figcaption><p>Script Line Chart</p></figcaption></figure>

The script line chart widget displays a chart based on data from the last run of a script. The script needs to output data in a particular format in order to define the chart's lines. Below is an example of how to generate data for a line chart.&#x20;

```powershell
1..5 | ForEach-Object {
    [PSCustomObject]@{ 
        type = "Category $_"
        value = Get-Random -Min 5 -Max 60
    }
}
```

In the properties for the line chart widget, set the XProperty to `type` and the YProperty to `value`.&#x20;

## Pre-built Widgets

You can find widgets created by Ironman Software and community members on the[ PowerShell Universal Gallery](../../platform/library.md).

## Custom Widgets

You can develop your own custom widgets using PSBlazor. PSBlazor employs Razor-like syntax combined with PowerShell to allow for creating fully interactive and customizable components.
