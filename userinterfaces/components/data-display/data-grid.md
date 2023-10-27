---
description: Data grid component for Universal Apps.
---

# Data Grid

The `UDDataGrid` component is an advanced version of the table that is useful for displaying large amounts of data. It supports many of the same features as the table but also provides complex filtering, row virtualization, multi-column sort and more.&#x20;

## Simple Data Grid

![](<../../../.gitbook/assets/image (150).png>)

Data grids load their data via the `-LoadRows` event handler. You will need to return a hashtable that contains the row data and the total number of rows.&#x20;

Columns are defined using hashtables.&#x20;

```powershell
New-UDDataGrid -LoadRows {
    $Data = @(
        @{ Name = 'Adam'; Number = Get-Random}
        @{ Name = 'Tom'; Number = Get-Random}
        @{ Name = 'Sarah'; Number = Get-Random}
    )
    $Rows| Out-UDDataGridData -Context $EventData -TotalRows $Rows.Length
} -Columns @(
    New-UDDataGridColumn -Field name
    New-UDDataGridColumn -Field number
) -AutoHeight $true
```

## Columns

Columns are customizable using hashtables. You can find the supported properties below.&#x20;

| Property          | Description                                                                                                                                                           | Type\Value                                       |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| Align             | How to align the data within the column.                                                                                                                              | Left, Center, Right                              |
| CellClassName     | A CSS class to apply to cells in this column                                                                                                                          | string                                           |
| ColSpan           | The number of columns this column should span.                                                                                                                        | Integer                                          |
| Description       | A tooltip description of the column                                                                                                                                   | string                                           |
| DisableColumnMenu | Disable the column menu for this column                                                                                                                               | boolean                                          |
| DisableExport     | Disable exporting of the data in this column                                                                                                                          | boolean                                          |
| Editable          | Whether or not this column can be edited                                                                                                                              | boolean                                          |
| Field             | The field (property) to use when displaying the value in the column.                                                                                                  | String                                           |
| Filterable        | Whether this column can be used in filters.                                                                                                                           | boolean                                          |
| Flex              | The `flex` property accepts a value between 0 and ∞. It works by dividing the remaining space in the grid among all flex columns in proportion to their `flex` value. | float                                            |
| HeaderAlign       | How to align header text.                                                                                                                                             | left, center, right                              |
| HeaderName        | The title to display in the header.                                                                                                                                   | String                                           |
| Hide              | Whether to hide the column                                                                                                                                            | boolean                                          |
| Hideable          | Whether a column can be hidden by the user.                                                                                                                           | boolean                                          |
| HideSortIcon      | Whether to hide the sort icon for the column                                                                                                                          | boolean                                          |
| MaxWidth          | The maximum width of the column                                                                                                                                       | integer                                          |
| MinWidth          | The minimum width of the column                                                                                                                                       | integer                                          |
| Pinnable          | Whether the column can be pinned.                                                                                                                                     | boolean                                          |
| Render            | A script block to render components in the column                                                                                                                     | ScriptBlock                                      |
| Resizable         | Whether the column can be resized                                                                                                                                     | boolean                                          |
| Sortable          | Whether the column can be sorted.                                                                                                                                     | boolean                                          |
| Type              | The type of data within the column                                                                                                                                    | string, number, date, dateTime, boolean, actions |
| Width             | How wide the column should be in pixels.                                                                                                                              | Integer                                          |

### Rendering Custom Columns

You can render custom components in columns by specifying `render` within the column hashtable. You can access the current row's data by using the `$EventData` or `$Row` variable

In this example, the number is shown in the name column with a `New-UDTypography` component.&#x20;

```powershell
New-UDDataGrid -LoadRows {  
    $Rows = 1..100 | % {
        @{ Name = 'Adam'; Number = Get-Random}
    }
    $Rows| Out-UDDataGridData -Context $EventData -TotalRows $Rows.Length
} -Columns @(
    New-UDDataGridColumn -Field name -Render {
         New-UDTypography $EventData.number 
    }
    New-UDDataGridColumn -Field number
) -AutoHeight $true
```

### Flexible Width Columns

Column fluidity or responsiveness can be achieved by setting the `flex` property of a column.

The `flex` property accepts a value between 0 and ∞. It works by dividing the remaining space in the grid among all flex columns in proportion to their `flex` value.

For example, consider a grid with a total width of 500px that has three columns: the first with `width: 200`; the second with `flex: 1`; and the third with `flex: 0.5`. The first column will be 200px wide, leaving 300px remaining. The column with `flex: 1` is twice the size of `flex: 0.5`, which means that final sizes will be: 200px, 200px, 100px.

To set a minimum and maximum width for a `flex` column set the `minWidth` and the `maxWidth` property on the column.

```powershell
New-UDDataGrid -LoadRows {  
    $Rows = 1..100 | % {
        @{ Name = 'Adam'; Number = "This column is a very long string. This column is a very long string. This column is a very long string. This column is a very long string. This column is a very long string. This column is a very long string."}
    }        
    $Rows| Out-UDDataGridData -Context $EventData -TotalRows $Rows.Length
} -Columns @(
    New-UDDataGridColumn -Field name -Render {
         New-UDTypography $EventData.number 
    }
    New-UDDataGridColumn -Field number -Flex 1.0
) -AutoHeight $true
```

## LoadRows

The `-LoadRows` parameter is used to return data for the data grid. Table state will be provided to the event handler as `$EventData`. You will find the following properties within the `$EventData` object.&#x20;

| Property | Description                                                               | Type      |
| -------- | ------------------------------------------------------------------------- | --------- |
| Filter   | A filter object that you can use to construct filters against your data.  | Hashtable |
| Page     | The current page. Starts at 0.                                            | Integer   |
| PageSize | The number of records in a page.                                          | Integer   |
| Sort     | The sort options for the table                                            | Hashtable |

### Paging

To implement paging, you can access the `page` and `pageSize` properties of the `$EventData` variable. Out-UDDataGridData automatically implements paging.

```powershell
New-UDDataGrid -LoadRows {  
    $Rows = 1..100 | % {
        @{ Name = 'Adam'; Number = Get-Random}
    } 
    $Rows| Out-UDDataGridData -Context $EventData -TotalRows $Rows.Length
} -Columns @(
    New-UDDataGridColumn -Field name
    New-UDDataGridColumn -Field number
) -AutoHeight $true -Pagination
```

### Filtering

![](<../../../.gitbook/assets/image (374).png>)

The filter hashtable is included in the `$EventData` for the `-LoadRows` event handler when a filter is defined. The hashtable has a structure as follows.&#x20;

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

![](<../../../.gitbook/assets/image (389).png>)

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

<figure><img src="../../../.gitbook/assets/image (192).png" alt=""><figcaption></figcaption></figure>

You can use the `-LoadDetailedContent` event handler to display additional information about the row you are expanding. Information about the current row is available in `$EventData.row`.

```powershell
New-UDDataGrid -LoadRows {
    $Data = @(
        @{ Name = 'Adam'; Number = Get-Random }
        @{ Name = 'Tom'; Number = Get-Random }
        @{ Name = 'Sarah'; Number = Get-Random }
    )
    $Data| Out-UDDataGridData -Context $EventData -TotalRows $Data.Length
} -Columns @(
    New-UDDataGridColumn -Field name
    New-UDDataGridColumn -Field number
) -AutoHeight $true -LoadDetailContent {
    Show-UDToast $Body
    New-UDAlert -Text $EventData.row.Name
}
```

## Editing

Tables provide editor support by specifying the `-OnEdit` event handler. The new row data will be provided as `$EventData`. You can chose to return updated row information (for example, adjusting something the user has entered) and return it from the event handler. If you do not return anything, the row will reflect what the user entered.&#x20;

The `$EventData` has the following format.&#x20;

```powershell
@{
    newRow = @{}
    oldRow = @{}
}
```

Ensure that you provide the `editable` property to each column you wish for the user to edit.&#x20;

```powershell
New-UDDataGrid -LoadRows {
    $Data = @(
        @{ Name = 'Adam'; number = Get-Random }
        @{ Name = 'Tom'; number = Get-Random }
        @{ Name = 'Sarah'; number = Get-Random }
    )
    $Data| Out-UDDataGridData -Context $EventData -TotalRows $Data.Length
} -Columns @(
    New-UDDataGridColumn -Field name -Editable
    New-UDDataGridColumn -Field number -Editable
) -AutoHeight $true -OnEdit {
    Show-UDToast "Editing $Body" 
}
```

## Custom Export

To override the default export functionality, use the `-OnExport` event handler. `$EventData` will be an array of rows with their values. You should use `Out-UDDataGridExport` to return the data from `-OnExport`.&#x20;

```powershell
New-UDDataGrid -LoadRows {
    $Data = @(
        @{ Name = 'Adam'; Number = Get-Random}
        @{ Name = 'Tom'; Number = Get-Random}
        @{ Name = 'Sarah'; Number = Get-Random}
    )
    $Data| Out-UDDataGridData -Context $EventData -TotalRows $Data.Length
} -Columns @(
    New-UDDataGridColumn -Field name
    New-UDDataGridColumn -Field number
) -AutoHeight $true -OnExport {
    $Data = $EventData | Select-Object -Expand name 
    Out-UDDataGridExport -Data $Data -FileName 'export.txt' | Out-String
}
```

## Example: Static Data

In this example, we generate an array of 10,000 records. We will create a new function, `Out-UDDataGridData` to manage the paging, sorting and filtering. This function is already included in the Universal module.&#x20;

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
        $simpleFilter = @()
        if($null -ne $Context.Filter.Items -and $Context.Filter.Items.Count -gt 0) {
            $linkOperator = $Context.Filter.linkOperator
            $count = 1
            $filterTextArray = @()
            foreach($filter in $Context.Filter.Items) {
                $property = $Filter.columnField
                $val = $filter.Value
                switch ($filter.operatorValue) {
                    "contains" { $filterTextArray += "obj.$property -like ""*$val*""" }
                    "equals" { $filterTextArray += "obj.$property -eq ""*$val*""" }
                    "startsWith" { $filterTextArray += "obj.$property -like ""$val*""" }
                    "endsWith" { $filterTextArray += "obj.$property -like ""*$val""" }
                    "isAnyOf" { $filterTextArray += "obj.$property -in ""$val""" }
                    "notequals" {$filterTextArray += "obj.$property -ne ""$val""" }
                    "notcontains" { $filterTextArray += "obj.$property -notlike ""*$val*""" }
                    "isEmpty" { $filterTextArray += "obj.$property -eq null" }
                    "isNotEmpty" { $filterTextArray += "obj.$property -ne null" }
                }
            }
            if ($linkOperator -eq 'and') {
                [string]$filterTextLine = $filterTextArray -join " -and "
            } else {
                [string]$filterTextLine = $filterTextArray -join " -or "
            }

            $filterTextLine = $filterTextLine.Replace('obj','$_')
            $filterTextLine = $filterTextLine.Replace('null','$null')
            $filterScriptBlock = [Scriptblock]::Create($filterTextLine)
            $Items = $Items | Where-Object -FilterScript $filterScriptBlock
        }

        if ($null -ne $Items) {
            $TotalRows = $Items.Count
        } else {
            $TotalRows = 0
        }

        $Sort = $Context.Sort[0]
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
    ) -AutoHeight $true -Pagination
}   
```

<figure><img src="../../../.gitbook/assets/image (356).png" alt=""><figcaption></figcaption></figure>

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
        $simpleFilter = @()
        if($null -ne $Context.Filter.Items -and $Context.Filter.Items.Count -gt 0) {
            $linkOperator = $Context.Filter.linkOperator #The link operator is 'AND' or 'OR'. It will always be one or the other for all properties
            foreach ($item in $Context.Filter.Items) {         
                $simpleFilter += [PSCustomObject]@{
                    Property    = $item.columnField
                    Value       = $item.Value
                    Operator    = $item.operatorValue
                }
            }
        }

        if($null -ne $simpleFilter -and $simpleFilter.Count -gt 0) {
            $count = 1
            foreach($filter in $simpleFilter) {
                if ($count -gt 1) {
                    $SqlFilter += " $($linkOperator) "
                } else {
                    $SqlFilter += " WHERE "
                }
                switch ($filter.Operator) {
                    "contains" { $SqlFilter += " $($filter.Property) LIKE '%$($filter.Value)%' " }
                    "equals" { $SqlFilter += " $($filter.Property) = '$($filter.Value)' " }
                    "startsWith" { $SqlFilter += " $($filter.Property) LIKE '$($filter.Value)%' " }
                    "endsWith" { $SqlFilter += " $($filter.Property) LIKE '%$($filter.Value)' " }
                    "isAnyOf" {
                        $count = 1
                        foreach($val in $filter.Value){
                            if($count -gt 1) {
                                $list += ", '$val'"
                            } else {
                                $list += "'$val'"
                            }  
                            $count += 1
                        }
                        $SqlFilter += " $($filter.Property) IN ($($list)) "
                    }
                    "isempty" { $SqlFilter += " TRIM ($($filter.Property)) IS NULL " }
                    "isnotempty" { $SqlFilter += " TRIM ($($filter.Property)) IS NOT NULL " }
                    "notequals" { $SqlFilter += " $($filter.Property) != '$($filter.Value)' " }
                    "notcontains" { $SqlFilter += " $($filter.Property) NOT LIKE '%$($filter.Value)%' " }
                }
                $count += 1
            }
        } else {
            $SqlFilter = $null
        }
        $totalCount = (Invoke-DbaQuery -SqlInstance $SqlInstance -Database $Database -Query "SELECT COUNT(*) As Count FROM $Table $SqlFilter" -SqlParameters $SqlParameters).Count
        $sort = $Context.Sort.'0'
        if ($sort)
        {
            $sqlSort = "ORDER BY $($sort.field) $($sort.Sort) "
        } else {
            $sqlSort = "ORDER BY (SELECT NULL)"
        }
        $sqlPage = "OFFSET $($Context.Page * $Context.PageSize) ROWS FETCH NEXT $($Context.PageSize) ROWS ONLY;"
        if($null -ne $SqlFilter) {
            $Query = "SELECT * FROM $Table $sqlFilter $sqlSort $sqlPage"
        } else {
            $Query = "SELECT * FROM $Table $sqlSort $sqlPage"
        }
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
    ) -AutoHeight $true -Pagination
}
```

<figure><img src="../../../.gitbook/assets/image (499).png" alt=""><figcaption></figcaption></figure>
