---
description: Data grid component for Universal Dashboard.
---

# Data Grid

The `UDDataGrid` component is an advanced version of the table that is useful for displaying large amounts of data. It supports many of the same features as the table but also provides complex filtering, row virtualization, multi-column sort and more.&#x20;

## Simple Data Grid

![](<../../../../.gitbook/assets/image (5).png>)

Data grids load their data via the `-LoadRows` event handler. You will need to return a hashtable that contains the row data and the total number of rows.&#x20;

Columns are defined using hashtables.&#x20;

{% hint style="warning" %}
Column field names must be in camel case. For example, the property `Name` would need to be `name` while the property `FirstName` would need to be `firstName`.
{% endhint %}

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

## Columns

Columns are customizable using hashtables. You can find the supported properties below.&#x20;

| Property          | Description                                                          | Type\Value                                       |
| ----------------- | -------------------------------------------------------------------- | ------------------------------------------------ |
| Align             | How to align the data within the column.                             | Left, Center, Right                              |
| CellClassName     | A CSS class to apply to cells in this column                         | string                                           |
| ColSpan           | The number of columns this column should span.                       | Integer                                          |
| Description       | A tooltip description of the column                                  | string                                           |
| DisableColumnMenu | Disable the column menu for this column                              | boolean                                          |
| DisableExport     | Disable exporting of the data in this column                         | boolean                                          |
| Editable          | Whether or not this column can be edited                             | boolean                                          |
| Field             | The field (property) to use when displaying the value in the column. | String                                           |
| Filterable        | Whether this column can be used in filters.                          | boolean                                          |
| HeaderAlign       | How to align header text.                                            | left, center, right                              |
| HeaderName        | The title to display in the header.                                  | String                                           |
| Hide              | Whether to hide the column                                           | boolean                                          |
| Hideable          | Whether a column can be hidden by the user.                          | boolean                                          |
| HideSortIcon      | Whether to hide the sort icon for the column                         | boolean                                          |
| MaxWidth          | The maximum width of the column                                      | integer                                          |
| MinWidth          | The minimum width of the column                                      | integer                                          |
| Pinnable          | Whether the column can be pinned.                                    | boolean                                          |
| Render            | A script block to render components in the column                    | ScriptBlock                                      |
| Resizable         | Whether the column can be resized                                    | boolean                                          |
| Sortable          | Whether the column can be sorted.                                    | boolean                                          |
| Type              | The type of data within the column                                   | string, number, date, dateTime, boolean, actions |
| Width             | How wide the column should be in pixels.                             | Integer                                          |

### Rendering Custom Columns

You can render custom components in columns by specifying `render` within the column hashtable. You can access the current row's data by using the `$EventData` or `$Row` variable

In this example, the number is shown in the name column with a `New-UDTypography` component.&#x20;

```powershell
New-UDDataGrid -LoadRows {  
    $Rows = 1..100 | % {
        @{ Name = 'Adam'; Number = Get-Random}
    }
    @{
        rows = $Rows
        rowCount = $Rows.Length
    }
    
} -Columns @(
    @{ field = "name"; render = { New-UDTypography $EventData.number }}
    @{ field = "number"}
) -AutoHeight
```

## LoadData

The `-LoadData` parameter is used to return data for the data grid. Table state will be provided to the event handler as `$EventData`. You will find the following properties within the `$EventData` object.&#x20;

| Property | Description                                                               | Type      |
| -------- | ------------------------------------------------------------------------- | --------- |
| Filter   | A filter object that you can use to construct filters against your data.  | Hashtable |
| Page     | The current page. Starts at 0.                                            | Integer   |
| PageSize | The number of records in a page.                                          | Integer   |
| Sort     | The sort options for the table                                            | Hashtable |

### Paging

To implement paging, you can access the `page` and `pageSize` properties of the `$EventData` variable.&#x20;

```powershell
New-UDDataGrid -LoadRows {  
    $Rows = 1..100 | % {
        @{ Name = 'Adam'; Number = Get-Random}
    } 
    @{
        rows = $Rows | Select-Object -First $EventData.pageSize -Skip ($EventData.page * $EventData.pageSize)
        rowCount = $Rows.Length
    }
    
} -Columns @(
    @{ field = "name"; }
    @{ field = "number"}
) -AutoHeight -Pagination
```

### Filtering

![](<../../../../.gitbook/assets/image (4).png>)

The filter hashtable is included in the `$EventData` for the `-LoadData` event handler when a filter is defined. The hashtable has a structure as follows.&#x20;

```powershell
@{
    items = @(
        @{ 
            columnField = "Name"
            overatorValue = "contains"
            value = "test"
        }
    )
    linkOperator = "and"
}
```

#### Items&#x20;

The items property contains an array of columns, operators and values. You can use these to filter your data.&#x20;

| Property      | Description                                           | Type   |
| ------------- | ----------------------------------------------------- | ------ |
| ColumnField   | The name of the field to filter                       | String |
| OperatorValue | The type of operator to use when filtering the data.  | String |
| Value         | The value used to filter                              | Object |

#### LinkOperator

The link operator field is used to specify the link between the filters. This can be `and` or `or`.&#x20;

### Sorting

![](<../../../../.gitbook/assets/image (2) (1).png>)

The `$EventData` object will contain a `Sort` property when the user sorts the data grid. It contains properties for each column that is sorted. The properties will start as 0 and increment as more columns are sorted.&#x20;

For example, you can access the first sorted column as follows.&#x20;

```powershell
$EventData.Sort.'0'.field
```

You will also receive the sort direction for each column.&#x20;

| Property | Description                      | Type      |
| -------- | -------------------------------- | --------- |
| Field    | The field to sort.               | String    |
| Sort     | The direction to sort the field. | asc, desc |

## Detailed Content&#x20;

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

You can use the `-LoadDetailedContent` event handler to display additional information about the row you are expanding. Information about the current row is available in `$EventData.row`.

```powershell
New-UDDataGrid -LoadRows {
    $Data = @(
        @{ Name = 'Adam'; Number = Get-Random }
        @{ Name = 'Tom'; Number = Get-Random }
        @{ Name = 'Sarah'; Number = Get-Random }
    )
    @{
        rows     = $Data 
        rowCount = $Data.Length
    }
} -Columns @(
    @{ field = "Name" }
    @{ field = "number" }
) -AutoHeight -LoadDetailContent {
    Show-UDToast $Body
    New-UDAlert -Text $EventData.row.Name
}
```



## Example: Static Data

In this example, we generate an array of 10,000 records. We will create a new function, `Out-UDDataGridData` to manage the paging, sorting and filtering.&#x20;

```powershell
function Out-UDDataGridData {
    param(
        [Parameter(Mandatory)]
        $Context, 
        [Parameter(Mandatory, ValueFromPipeline)]
        [object]$Data, 
        [Parameter()]
        [int]$TotalRows = -1
    )

    Begin {
        $Items = [System.Collections.ArrayList]::new()
    }

    Process {
        $Items.Add($Data) | Out-Null
    }

    End {
        if ($TotalRows  -eq -1)
        {
            $TotalRows = $Items.Count
        }

        $Filter = $Context.Filter 
        foreach ($item in $Filter.Items) {
            $Property = $item.columnField
            $Value = $item.Value
            switch ($item.operatorValue) {
                "contains" { $Items = $Items | Where-Object {  $_[$Property].ToString().Contains($Value)}; } 
                "equals" { $Items = $Items | Where-Object {  $_[$Property].ToString() -eq $Value } }  
                "startsWith" { $Items = $Items | Where-Object { $_[$Property].ToString().StartsWith($Value)} }
                "endsWith" { $Items = $Items | Where-Object { $_[$Property].ToString().EndsWiths($Value)} }
                "isEmpty" { $Items = $Items | Where-Object { [string]::IsNullOrEmpty($_[$Property].ToString()) } }
                "isNotEmpty" { $Items = $Items | Where-Object { -not [string]::IsNullOrEmpty($_[$Property].ToString()) } }
                "isAnyOf" { $Items = $Items | Where-Object { $_[$Property].ToString() -in $Value } }
            }
        }

        $Sort = $Context.Sort.'0'
        $Items = $Items | Sort-Object -Property $Sort.field -Descending:$($Sort.Sort -eq 'desc')

        $Items = $Items | Select-Object -Skip ($Context.Page * $Context.pageSize) -First $Context.PageSize

        @{
            rows     = [Array]$Items 
            rowCount = $TotalRows
        }
    }    
}

New-UDDashboard -Title 'PowerShell Universal' -Content {
     $Data =  1..10000 | % {
        @{ Name = 'Adam'; Number = Get-Random }
    } 
    New-UDDataGrid -LoadRows {  
      $Data | Out-UDDataGridData -Context $EventData
    } -Columns @(
        @{ field = "name"; render = { 
            New-UDButton -Icon (New-UDIcon -Icon User) -OnClick { Show-UDToast $EventData.Name } } 
        }
        @{ field = "number" }
    ) -AutoHeight -Pagination
}
```

<figure><img src="../../../../.gitbook/assets/image (6) (3).png" alt=""><figcaption></figcaption></figure>

## Example: SQL Data

In this example, we'll query the PowerShell Universal database with dbatools.&#x20;

```powershell
function Out-UDSQLDataGrid {
    param(
        [Parameter(Mandatory)]
        $Context, 
        [Parameter(Mandatory)]
        [string]$Table, 
        [Parameter(Mandatory)]
        [string]$SqlInstance,
        [Parameter(Mandatory)]
        [string]$Database
    )

    End {

        $SqlFilter = "WHERE "        
        $SqlParameters = @{}
        $Filter = $Context.Filter 
        foreach ($item in $Filter.Items) {
            $Property = $item.columnField
            $Value = $item.Value

            $Parameter = "Param" + $SqlParameters.Count
            
            if ($item.operatorValue -eq 'contains')
            {
                $SqlParameters.Add($Parameter, "%$Value%") | Out-Null
            } 
            else 
            {
                $SqlParameters.Add($Parameter, $Value) | Out-Null            
            }
            
            switch ($item.operatorValue) {
                "contains" { $SqlFilter += "$Property LIKE $Parameter AND " } 
                "equals" { $SqlFilter += "$Property = $Parameter AND " }  
                "isEmpty" { $SqlFilter += "$Property IS NULL "  }
                "isNotEmpty" { $SqlFilter += "$Property IS NOT NULL "  }
            }
        }

        $SQLFilter += " 1 = 1"

        $TotalCount = (Invoke-DbaQuery -SqlInstance $SqlInstance -Database $Database -Query "SELECT COUNT(*) As Count FROM $Table $SqlFilter" -SqlParameters $SqlParameters).Count 

        $Sort = $Context.Sort.'0'
        if ($Sort)
        {
            $SqlSort = "ORDER BY $($Sort.field) $($Sort.Sort) "
        }
        else 
        {
            $SqlSort = "ORDER BY 1 "
        }

        $SqlPage = "OFFSET $($Context.Page * $Context.PageSize) ROWS FETCH NEXT $($Context.PageSize) ROWS ONLY;"

        $Query = "SELECT * FROM $Table $SqlFilter $SqlSort $SqlPage"

        Show-UDToast $Query -Duration 50000

        $Rows = Invoke-DbaQuery -SqlInstance $SqlInstance -Database $Database -Query $Query -As PSObject -SqlParameters $SqlParameters

        @{
            rows     = [Array]$Rows
            rowCount = $TotalCount
        }
    }    
}

New-UDDashboard -Title 'PowerShell Universal' -Content {
    New-UDDataGrid -LoadRows {  
      Out-UDSqlDataGrid -Context $EventData -SqlInstance "(localdb)\MSSQLLocalDb" -Database "PSU" -Table "Job"
    } -Columns @(
        @{ field = "id"; }
        @{ field = "startTime"; }
        @{ field = "status"; render = {
            if ($EventData.Status -eq 2) {
                New-UDAlert -Severity 'Success' -Text 'Success'
            }

            if ($EventData.Status -eq 3) {
                New-UDAlert -Severity 'Error' -Text 'Failed'
            }
        } }
    ) -AutoHeight -Pagination
}
```

<figure><img src="../../../../.gitbook/assets/image (6) (2).png" alt=""><figcaption></figcaption></figure>
