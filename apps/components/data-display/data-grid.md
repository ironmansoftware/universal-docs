---
description: Data grid component for Universal Apps.
---

# Data Grid

The `UDDataGrid` component is an advanced version of the table that is useful for displaying large amounts of data. It supports many of the same features as the table but also provides complex filtering, row virtualization, multi-column sort and more.

## Simple Data Grid

![](<../../../.gitbook/assets/image (150).png>)

Data grids load their data via the `-LoadRows` event handler. You will need to return a hashtable that contains the row data and the total number of rows.

Columns are defined using hashtables.

```powershell
New-UDDataGrid -LoadRows {
    $Data = @(
        @{ Name = 'Adam'; Number = Get-Random}
        @{ Name = 'Tom'; Number = Get-Random}
        @{ Name = 'Sarah'; Number = Get-Random}
    )
    $Data | Out-UDDataGridData -Context $EventData -TotalRows $Rows.Length
} -Columns @(
    New-UDDataGridColumn -Field name
    New-UDDataGridColumn -Field number
) -AutoHeight $true
```

## Columns

Columns are customizable using `New-UDDataGridColumn`. More information on this cmdlet can be found [here](../../../cmdlets/New-UDDataGridColumn.txt).

### Rendering Custom Columns

You can render custom components in columns by specifying `render` within the column hashtable. You can access the current row's data by using the `$EventData` or `$Row` variable

In this example, the number is shown in the name column with a `New-UDTypography` component.

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

The `-LoadRows` parameter is used to return data for the data grid. Table state will be provided to the event handler as `$EventData`. You will find the following properties within the `$EventData` object.

| Property | Description                                                              | Type      |
| -------- | ------------------------------------------------------------------------ | --------- |
| Filter   | A filter object that you can use to construct filters against your data. | Hashtable |
| Page     | The current page. Starts at 0.                                           | Integer   |
| PageSize | The number of records in a page.                                         | Integer   |
| Sort     | The sort options for the table                                           | Hashtable |

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

The filter hashtable is included in the `$EventData` for the `-LoadRows` event handler when a filter is defined. The hashtable has a structure as follows.

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

#### Items

The items property contains an array of columns, operators and values. You can use these to filter your data.

| Property      | Description                                          | Type   |
| ------------- | ---------------------------------------------------- | ------ |
| ColumnField   | The name of the field to filter                      | String |
| OperatorValue | The type of operator to use when filtering the data. | String |
| Value         | The value used to filter                             | Object |

#### LinkOperator

The link operator field is used to specify the link between the filters. This can be `and` or `or`.

### Sorting

![](<../../../.gitbook/assets/image (389).png>)

The `$EventData` object will contain a `Sort` property when the user sorts the data grid. It contains properties for each column that is sorted. The properties will start as 0 and increment as more columns are sorted.

For example, you can access the first sorted column as follows.

```powershell
$EventData.Sort.'0'.field
```

You will also receive the sort direction for each column.

| Property | Description                      | Type      |
| -------- | -------------------------------- | --------- |
| Field    | The field to sort.               | String    |
| Sort     | The direction to sort the field. | asc, desc |

## Detailed Content

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

Tables provide editor support by specifying the `-OnEdit` event handler. The new row data will be provided as `$EventData`. You can chose to return updated row information (for example, adjusting something the user has entered) and return it from the event handler. If you do not return anything, the row will reflect what the user entered.

The `$EventData` has the following format.

```powershell
@{
    newRow = @{}
    oldRow = @{}
}
```

Ensure that you provide the `editable` property to each column you wish for the user to edit.

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

To override the default export functionality, use the `-OnExport` event handler. `$EventData` will be the same context object used for `-LoadRows`. You should use `Out-UDDataGridExport` to return the data from `-OnExport`.

```powershell
$Data = @(
    @{ name = 'Adam'; Number = Get-Random}
    @{ name = 'Tom'; Number = Get-Random}
    @{ name = 'Sarah'; Number = Get-Random}
)

New-UDDataGrid -LoadRows {
    @{
        rows = $Data 
        rowCount = $Data.Length
    }
} -Columns @(
    New-UDDataGridColumn -Field name
    New-UDDataGridColumn -Field number
) -OnExport {
    $ExportContent = $Data | ConvertTo-Csv -NoTypeInformation | Out-String
    Out-UDDataGridExport -Data $ExportContent -FileName 'export.csv' 
}
```

## Example: Static Data

In this example, we generate an array of 10,000 records. We will create a new function, `Out-UDDataGridData` to manage the paging, sorting and filtering. This function is already included in the [Universal module](../../../cmdlets/Out-UDDataGridData.txt).

```powershell
New-UDDashboard -Title 'PowerShell Universal' -Content {
     $Data =  1..10000 | % {
        @{ Name = 'Adam'; Number = Get-Random }
    } 
    New-UDDataGrid -LoadRows {  
      $Data | Out-UDDataGridData -Context $EventData
    } -Columns @(
        New-UDDataGridColumn -Field name
        New-UDDataGridColumn -Field number -Render {
                    New-UDButton -Icon (New-UDIcon -Icon User) -OnClick { Show-UDToast $EventData.Name } } 
        }
    ) -AutoHeight $true -Pagination
}   
```

<figure><img src="../../../.gitbook/assets/image (356).png" alt=""><figcaption></figcaption></figure>

## Example: SQL Data

In this example, we'll query the PowerShell Universal database with dbatools.

```powershell
function Out-UDSQLDataGrid {
    param(
        $Context,
        [Parameter(Mandatory)]
        [string]$Table,
        [Parameter(Mandatory)]
        [string]$SqlInstance,
        [Parameter(Mandatory)]
        [string]$Database,
        [Parameter(Mandatory)]
        [pscredential]$SqlCredential,
        [Int32]$RowsPerPage
    )

    End {
        $simpleFilter = @()

        if ($null -ne $Context.Filter.Items -and $Context.Filter.Items.Count -gt 0) {
            $logicOperator = $Context.Filter.logicOperator #The link operator is 'AND' or 'OR'. It will always be one or the other for all properties

            foreach ($item in $Context.Filter.Items) {         
                $simpleFilter += [PSCustomObject]@{
                    Property = $item.Field
                    Value    = $item.Value
                    Operator = $item.Operator
                }
            }
        }

        if ($null -ne $simpleFilter -and $simpleFilter.Count -gt 0) {
            $count = 1
            foreach ($filter in $simpleFilter) {
                if ($count -gt 1) {               
                    $SqlFilter += " $($logicOperator) "
                }
                else {
                    $SqlFilter += " WHERE "
                }

                switch ($filter.Operator) {
                    "contains" { $SqlFilter += " $($filter.Property) LIKE '%$($filter.Value)%' " }
                    "equals" { $SqlFilter += " $($filter.Property) = '$($filter.Value)' " }
                    "startsWith" { $SqlFilter += " $($filter.Property) LIKE '$($filter.Value)%' " }
                    "endsWith" { $SqlFilter += " $($filter.Property) LIKE '%$($filter.Value)' " }
                    "isAnyOf" {
                        $count = 1
                        foreach ($val in $filter.Value) {
                            if ($count -gt 1) {
                                $list += ", '$val'"
                            }
                            else {
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
        }
        else {
            $SqlFilter = $null
        }

        if ($null -eq $SqlFilter) {
            $totalCount = (Invoke-DbaQuery -SqlInstance $SqlInstance -Database $Database -SqlCredential $SqlCredential -Query "SELECT COUNT(*) As Count FROM $Table").Count
        }
        else {
            $totalCount = (Invoke-DbaQuery -SqlInstance $SqlInstance -Database $Database -SqlCredential $SqlCredential -Query "SELECT COUNT(*) As Count FROM $Table $SqlFilter").Count
            $sort = $Context.Sort.'0'
        }

        if ($sort) {
            $sqlSort = "ORDER BY $($sort.field) $($sort.Sort) "
        }
        else {
            $sqlSort = "ORDER BY (SELECT NULL)"
        }

        if ($null -ne $SqlFilter) {
            $sqlPage = "OFFSET $($Context.Page * $Context.PageSize) ROWS FETCH NEXT $($Context.PageSize) ROWS ONLY;"
            $Query = "SELECT * FROM $Table $sqlFilter $sqlSort $sqlPage"
        }
        else {
            $sqlPage = "OFFSET $($RowsPerPage) ROWS FETCH NEXT $($RowsPerPage) ROWS ONLY;"
            $Query = "SELECT * FROM $Table $sqlSort $sqlPage"
        }

        $Rows = Invoke-DbaQuery -SqlInstance $SqlInstance -Database $Database -SqlCredential $SqlCredential -Query $Query -As PSObject

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
        New-UDDataGridColumn -Field id
        New-UDDataGridColumn -Field startTime
        New-UDDataGridColumn -Field status -Render {
          if ($EventData.Status -eq 2) {
                New-UDAlert -Severity 'Success' -Text 'Success'
            }

            if ($EventData.Status -eq 3) {
                New-UDAlert -Severity 'Error' -Text 'Failed'
            }
        }
    ) -AutoHeight $true -Pagination
}
```

<figure><img src="../../../.gitbook/assets/image (499).png" alt=""><figcaption></figcaption></figure>

## API

* [New-UDDataGrid](../../../cmdlets/New-UDDataGrid.txt)
* [New-UDDataGridColumn](../../../cmdlets/New-UDDataGridColumn.txt)
* [Out-UDDataGridData](../../../cmdlets/Out-UDDataGridData.txt)
* [Out-UDDataGridExport](../../../cmdlets/Out-UDDataGridExport.txt)
