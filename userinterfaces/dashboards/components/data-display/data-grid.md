---
description: Data grid component for Universal Dashboard.
---

# Data Grid

{% hint style="info" %}
The data grid component is coming in PowerShell Universal 3.2.
{% endhint %}

The `UDDataGrid` component is an advanced version of the table that is useful for displaying large amounts of data. It supports many of the same features as the table but also providers complex filtering, row virtualization and more.&#x20;

## Simple Data Grid

Data grids load their data via the `-LoadRows` event handler. You will need to return a hashtable that contains the row data and the total number of rows.&#x20;

Columns are defined using hashtables.&#x20;

```powershell
New-UDDataGrid -LoadRows {
    $Data = @(
        @{ Name = 'Adam'; Number = Get-Random}
        @{ Name = 'Tom'; Number = Get-Random}
        @{ Name = 'Sarah'; Number = Get-Random}
    )
    @{
        rows = $Data 
        rowCount = $Data.Length
    }
} -Columns @(
    @{ field = "name"}
    @{ field = "number"}
) -AutoHeight
```

