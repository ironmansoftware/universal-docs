---
description: Table component for Universal Apps
---

# Table

Tables display sets of data. They can be fully customized.

Tables display information in a way that’s easy to scan, so that users can look for patterns and insights. They can be embedded in primary content, such as cards.

## Simple Table

![](<../../../.gitbook/assets/image (300).png>)

A simple example with no frills. Table columns are defined from the data.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
)

New-UDTable -Data $TableData
```

## Table with Custom Columns

![](<../../../.gitbook/assets/image (510).png>)

Define custom columns for your table.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

$Columns = @(
    New-UDTableColumn -Property Dessert -Title "A Dessert"
    New-UDTableColumn -Property Calories -Title Calories 
    New-UDTableColumn -Property Fat -Title Fat 
    New-UDTableColumn -Property Carbs -Title Carbs 
    New-UDTableColumn -Property Protein -Title Protein 
)

New-UDTable -Id 'customColumnsTable' -Data $TableData -Columns $Columns
```

## Table with Custom Column Rendering

![](<../../../.gitbook/assets/image (289).png>)

Define column rendering. Sorting and exporting still work for the table.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 1; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 200; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

$Columns = @(
    New-UDTableColumn -Property Dessert -Title Dessert -Render { 
        New-UDButton -Id "btn$($EventData.Dessert)" -Text "Click for Dessert!" -OnClick { Show-UDToast -Message $EventData.Dessert } 
    }
    New-UDTableColumn -Property Calories -Title Calories 
    New-UDTableColumn -Property Fat -Title Fat 
    New-UDTableColumn -Property Carbs -Title Carbs 
    New-UDTableColumn -Property Protein -Title Protein 
)

New-UDTable -Data $TableData -Columns $Columns -Sort -Export
```

## Table Column Width

Column width can be defined using the `-Width` parameter. You can also decide to truncate columns that extend past that width.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

$Columns = @(
    New-UDTableColumn -Property Dessert -Title Dessert -Render { 
        New-UDButton -Id "btn$($EventData.Dessert)" -Text "Click for Dessert!" -OnClick { Show-UDToast -Message $EventData.Dessert } 
    }
    New-UDTableColumn -Property Calories -Title Calories -Width 5 -Truncate
    New-UDTableColumn -Property Fat -Title Fat 
    New-UDTableColumn -Property Carbs -Title Carbs 
    New-UDTableColumn -Property Protein -Title Protein 
)

New-UDTable -Data $TableData -Columns $Columns -Sort
```

## Filters

You can configure custom filters per column. The table supports `text`, `select`, `fuzzy` , `slider`, `range`, `date` , `number`, and `autocomplete` filters.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

$Columns = @(
    New-UDTableColumn -Property Dessert -Title "A Dessert" -Filter -FilterType AutoComplete
    New-UDTableColumn -Property Calories -Title Calories -Filter -FilterType Range
    New-UDTableColumn -Property Fat -Title Fat -Filter -FilterType Range
    New-UDTableColumn -Property Carbs -Title Carbs -Filter -FilterType Range
    New-UDTableColumn -Property Protein -Title Protein -Filter -FilterType Range
)

New-UDTable -Id 'customColumnsTable' -Data $TableData -Columns $Columns -ShowFilter
```

![](<../../../.gitbook/assets/image (445).png>)

### Static Options for Select Filters

When using server-side processing, the available filters may not display the full range of options since the select dropdown only has access to the current page of results. To avoid this, you can use the `-Options` parameter on `New-UDTableColumn`.

```powershell
New-UDTableColumn -Property Dessert -Title 'Dessert' -Filter -FilterType 'Select' -Options @('Frozen yoghurt', 'Eclair', 'Cupcake')
```

## Search

To enable search, use the `-ShowSearch` parameter on `New-UDTable`.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
)

New-UDTable -Data $TableData -ShowSearch
```

When using custom columns, you will need to add the `-IncludeInSearch` parameter to the columns you'd like to include in the search.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

$Columns = @(
    New-UDTableColumn -Property Dessert -Title "A Dessert" -IncludeInSearch
    New-UDTableColumn -Property Calories -Title Calories 
    New-UDTableColumn -Property Fat -Title Fat 
    New-UDTableColumn -Property Carbs -Title Carbs 
    New-UDTableColumn -Property Protein -Title Protein 
)

New-UDTable -Id 'customColumnsTable' -Data $TableData -Columns $Columns -ShowSearch
```

## Table with server-side processing

Process data on the server so you can perform paging, filtering, sorting and searching in systems like SQL. To implement a server-side table, you will use the `-LoadData` parameter. This parameter accepts a `ScriptBlock`. The `$EventData` variable includes information about the state of the table. You can use cmdlets to process the data based on this information.

### $EventData Structure

The `$EventData` object contains the following properties.

| Property Name  | Type                                                                              | Description                                                                 |
| -------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| Filters        | <p>Hashtable[]<br><br>@{<br>id = 'fieldName'</p><p>value = 'filterValue'<br>}</p> | A list of filter values. Each hashtable has an `Id` and a `Value` property. |
| OrderBy        | <p>Hashtable<br><br>@{ field = "fieldName" }</p>                                  | Property name to sort by.                                                   |
| OrderDirection | string                                                                            | `asc` or `desc` depending on the sort order.                                |
| Page           | int                                                                               | The current page (starting with 0).                                         |
| PageSize       | int                                                                               | The selected page size.                                                     |
| Properties     | string\[]                                                                         | An array of properties being shown in the table.                            |
| Search         | string                                                                            | A search string provided by the user.                                       |
| TotalCount     | int                                                                               | The total number of records before filtering or paging.                     |

### Example

```powershell
$Columns = @(
    New-UDTableColumn -Property Name -Title "Name" -ShowFilter
    New-UDTableColumn -Property Value -Title "Value" -ShowFilter
)

$TableData = 1..1000 | ForEach-Object {
  [PSCustomObject]@{
      Name = "Record-$_"
      Value = $_ 
  }
}

New-UDTable -Columns $Columns -LoadData {
    foreach($Filter in $EventData.Filters)
    {
        $TableData = $TableData | Where-Object -Property $Filter.Id -Match -Value $Filter.Value
    }
    
    if ($EventData.Search)
    {
        $TableData = $TableData | Where-Object { $_.Name -match $EventData.Search -or $_.Value -match $EventData.Search }
    }

    $TotalCount = $TableData.Count 

    if (-not [string]::IsNullOrEmpty($EventData.OrderBy.Field))
    {
        $Descending = $EventData.OrderDirection -ne 'asc'
        $TableData = $TableData | Sort-Object -Property ($EventData.orderBy.Field) -Descending:$Descending
    }
    
    $TableData = $TableData | Select-Object -First $EventData.PageSize -Skip ($EventData.Page * $EventData.PageSize)

    $TableData | Out-UDTableData -Page $EventData.Page -TotalCount $TotalCount -Properties $EventData.Properties 
} -ShowFilter -ShowSort -ShowPagination
```

### Retrieving Displayed Data

You may want to allow the user to take action on the current set of displayed data. To do so, use `Get-UDElement` in the input object you want to retrieve the data from and get the table by Id. Once you have the element, you can use the `Data` property of the element to get an array of currently displayed rows.

```powershell
$Columns = @(
    New-UDTableColumn -Property Name -Title "Name" -ShowFilter
    New-UDTableColumn -Property Value -Title "Value" -ShowFilter
)

$TableData = 1..1000 | ForEach-Object {
  @{
      Name = "Record-$_"
      Value = $_ 
  }
}

New-UDButton -Text 'Get Filtered Data' -OnClick {
    $Element = Get-UDElement -Id 'filteredTable'
    Show-UDModal -Content {
        New-UDElement -Tag 'pre' -Content {
           $Element | ConvertTo-Json
        }
    }
}

New-UDTable -Id 'filteredTable' -Columns $Columns -LoadData {
    foreach($Filter in $EventData.Filters)
    {
        $TableData = $TableData | Where-Object -Property $Filter.Id -Match -Value $Filter.Value
    }

    $TotalCount = $TableData.Count 

    if (-not [string]::IsNullOrEmpty($EventData.OrderBy))
    {
        $Descending = $EventData.OrderDirection -ne 'asc'
        $TableData = $TableData | Sort-Object -Property $EventData.orderBy -Descending:$Descending
    }
    
    $TableData = $TableData | Select-Object -First $EventData.PageSize -Skip ($EventData.Page * $EventData.PageSize)

    $TableData | Out-UDTableData -Page $EventData.Page -TotalCount $TotalCount -Properties $EventData.Properties 
} -ShowFilter -ShowSort -ShowPagination
```

## Paging

By default, paging is disable and tables will grow based on how many rows of data you provide. You can enable paging by using the `-ShowPagination` cmdlet (alias `-Paging`). You can configure the page size using the `-PageSize` cmdlet.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

New-UDTable -Data $TableData -Paging -PageSize 2
```

### Disable Page Size All

By default, the page size selector provides an option to show all rows. If you want to prevent users from doing this, use the `-DisablePageSizeAll` cmdlet.

### Pagination Location

You can change the location of the pagination control by using the `-PaginationLocation` parameter. It accepts top, bottom and both.

![Pagination Location](<../../../.gitbook/assets/image (77).png>)

### Page Sizes

The page size, by default, is set to 5. Users can adjust the number of rows per page by using the Rows per page drop down. You can adjust the default page size by using the `-PageSize` parameter. To adjust the values available within the Rows per page drop down, you can use an array of integers pass to the `-PageSizeOptions` parameter.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

New-UDTable -Data $TableData -Paging -PageSize 2 -PageSizeOptions @(2, 4, 6)
```

## Sorting

To enable sorting for a table, use the `-ShowSort` parameter. When you enable sorting, you will be able to click the table headers to sort the table by clicking the headers. By default, multi-sort is enabled. To multi-hold shift and click a column header.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

New-UDTable -Data $TableData -ShowSort
```

You can control which columns can be sorted by using `New-UDTableColumn` and `-ShowSort` parameter.

```powershell
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

$Columns = @(
    New-UDTableColumn -Property Dessert -Title "A Dessert" -ShowSort
    New-UDTableColumn -Property Calories -Title Calories 
    New-UDTableColumn -Property Fat -Title Fat 
    New-UDTableColumn -Property Carbs -Title Carbs -ShowSort
    New-UDTableColumn -Property Protein -Title Protein -ShowSort
)

New-UDTable -Id 'customColumnsTable' -Data $TableData -Columns $Columns
```

### Disable Sort Remove

By default, the sorting of a table has 3 states. Unsorted, ascending and descending. If you would like to disable the unsorted state, use the `-DisableSortRemove` parameter of `New-UDTable`.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

New-UDTable -Data $TableData -ShowSort -DisableSortRemove
```

## Selection

### Static Table Data

Tables support selection of rows. You can create an event handler for the `OnRowSelected` parameter to receive when a new row is selected or unselected or you can use `Get-UDElement` to retrieve the current set of selected rows.

The following example creates a table with row selection enabled. A toast is show when clicking the row or when clicking the GET Rows button.

```powershell
$TableData = try { get-service -ea Stop | select Name,@{n = "Status";e={ $_.Status.ToString()}},@{n = "StartupType";e={ $_.StartupType.ToString()}},@{n = "StartType";e={ $_.StartType.ToString()}} } catch {}
$Columns = @(
    New-UDTableColumn -Property Name -Title "Service Name" -ShowSort -IncludeInExport -IncludeInSearch -ShowFilter -FilterType text
    New-UDTableColumn -Property Status -Title Status -ShowSort -DefaultSortColumn -IncludeInExport -IncludeInSearch -ShowFilter -FilterType select 
    New-UDTableColumn -Property StartupType -Title StartupType -IncludeInExport -ShowFilter -FilterType select
    New-UDTableColumn -Property StartType -Title StartType -IncludeInExport -ShowFilter -FilterType select 
)
New-UDTable -Id 'service_table' -Data $TableData -Columns $Columns -Title 'Services' -ShowSearch -ShowPagination -ShowSelection -Dense -OnRowSelection {
    $Item = $EventData
    Show-UDToast -Message "$($Item | out-string)"
}
New-UDButton -Text "GET Rows" -OnClick {
    $value = Get-UDElement -Id "service_table"
    Show-UDToast -Message "$( $value.selectedRows | Out-String )"
}
```

![Row selection](../../../.gitbook/assets/table.gif)

The `$EventData` variable for the `-OnRowSelected` event will include all the columns as properties and a selected property as to whether the row was selected or unselected.

For example, the service table data would look like this.

```powershell
@{
   Id = 0
   Name = 'AESMService',
   Status = 'Running'
   StartupType = 'AutomaticDelayedStart'
   StartType = 'Automation'
   selected = $true
}
```

### Dynamic (Server-Side) Tables

When using selection and `-LoadData`, the `-OnRowSelected $EventData` will be the IDs of the rows and not the entire row data. It will still indicate where the row has been selected or de-selected.&#x20;

## Collapsible Rows

You can include additional information within the table by using the `-OnRowExpand` parameter of `New-UDTable`. It accepts a ScriptBlock that you can use to return additional components.

```powershell
New-UDTable -Data (Get-Service) -OnRowExpand {
    New-UDAlert -Text $EventData.DisplayName
} -Columns @(
    New-UDTableColumn -Title 'Name' -Property 'Name'
    New-UDTableColumn -Title 'Status' -Property 'Status'
)
```

![](<../../../.gitbook/assets/image (121).png>)

## Exporting

Tables support exporting the data within the table. You can export as CSV, XLSX, JSON or PDF. You can define which columns to include in an export and choose to export just the current page or all the data within the table.

```powershell
$TableData = try { get-service -ea Stop | select Name,@{n = "Status";e={ $_.Status.ToString()}},@{n = "StartupType";e={ $_.StartupType.ToString()}},@{n = "StartType";e={ $_.StartType.ToString()}} } catch {}
$Columns = @(
    New-UDTableColumn -Property Name -Title "Service Name" -IncludeInExport
    New-UDTableColumn -Property Status -Title Status 
    New-UDTableColumn -Property StartupType
    New-UDTableColumn -Property StartType -IncludeInExport
)
New-UDTable -Id 'service_table' -Data $TableData -Columns $Columns -Title 'Services' -ShowSearch -ShowPagination -Dense -Export
```

![](<../../../.gitbook/assets/image (31).png>)

### Hidden Columns

Hidden columns allow you to include data that is not displayed in the table but is included in the exported data.

The following hides the StartType column from the user but includes it in the export.

```powershell
$TableData = try { get-service -ea Stop | select Name,@{n = "Status";e={ $_.Status.ToString()}},@{n = "StartupType";e={ $_.StartupType.ToString()}},@{n = "StartType";e={ $_.StartType.ToString()}} } catch {}
$Columns = @(
    New-UDTableColumn -Property Name -Title "Service Name" -IncludeInExport
    New-UDTableColumn -Property Status -Title Status 
    New-UDTableColumn -Property StartupType
    New-UDTableColumn -Property StartType -IncludeInExport -Hidden
)
New-UDTable -Id 'service_table' -Data $TableData -Columns $Columns -Title 'Services' -ShowSearch -ShowPagination -Dense -Export
```

## Server-Side Exporting

You can control the export functionality with a PowerShell script block. This is useful when exporting from server-side sources like SQL server tables.

In this example, I have a SQL table that contains podcasts. When exporting, you will receive information about the current state of the table to allow you to customize what data is exported.

```powershell
$Columns = @(
    New-UDTableColumn -Property Name -Title "Name" -ShowFilter -IncludeInExport
    New-UDTableColumn -Property Value -Title "Value" -ShowFilter -IncludeInExport
)

$TableData = 1..1000 | ForEach-Object {
  [PSCustomObject]@{
      Name = "Record-$_"
      Value = $_ 
  }
}

New-UDTable -Columns $Columns -LoadData {
    foreach($Filter in $EventData.Filters)
    {
        $TableData = $TableData | Where-Object -Property $Filter.Id -Match -Value $Filter.Value
    }

    $TotalCount = $TableData.Count 

    if (-not [string]::IsNullOrEmpty($EventData.OrderBy.Field))
    {
        $Descending = $EventData.OrderDirection -ne 'asc'
        $TableData = $TableData | Sort-Object -Property ($EventData.orderBy.Field) -Descending:$Descending
    }
    
    $TableData = $TableData | Select-Object -First $EventData.PageSize -Skip ($EventData.Page * $EventData.PageSize)

    $TableData | Out-UDTableData -Page $EventData.Page -TotalCount $TotalCount -Properties $EventData.Properties 
} -ShowFilter -ShowSort -ShowPagination  -Export -OnExport {
   $Query = $Body | ConvertFrom-Json

        <# Query will contain
            filters: []
            orderBy: undefined
            orderDirection: ""
            page: 0
            pageSize: 5
            properties: (5) ["dessert", "calories", "fat", "carbs", "protein"]
            search: ""
            totalCount: 0
            allRows: true
        #>

    $TableData | ConvertTo-Json
}
```

## Customizing Export Options

You can decide which export options to present to your users using the `-ExportOption` cmdlet. The following example would only show the CSV export option.

```powershell
$TableData = try { get-service -ea Stop | select Name,@{n = "Status";e={ $_.Status.ToString()}},@{n = "StartupType";e={ $_.StartupType.ToString()}},@{n = "StartType";e={ $_.StartType.ToString()}} } catch {}
$Columns = @(
    New-UDTableColumn -Property Name -Title "Service Name" -IncludeInExport
    New-UDTableColumn -Property Status -Title Status 
    New-UDTableColumn -Property StartupType
    New-UDTableColumn -Property StartType -IncludeInExport
)
New-UDTable -Id 'service_table' -Data $TableData -Columns $Columns -Title 'Services' -ShowSearch -ShowPagination -Dense -Export -ExportOption "csv"
```

## Customizing Labels

You can use the `-TextOption` parameter along with the `New-UDTableTextOption` cmdlet to set text fields within the table.

```powershell
$TableData = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

$Option = New-UDTableTextOption -Search "Search all these records"

New-UDTable -Data $TableData -TextOption $Option -ShowSearch
```

## Refresh with a button

### Data Parameter

You can externally refresh a table by putting the table within a dynamic region and using `Sync-UDElement`.

This example creates a button to refresh the table.

```powershell
New-UDDynamic -Id 'table' -Content {
    $TableData = @(
        @{ Random = Get-Random }
        @{ Random = Get-Random }
        @{ Random = Get-Random }
        @{ Random = Get-Random }
        @{ Random = Get-Random }
    )
    
    # Store in the page so we can get the current ID. 
    # Using the same ID fails to update when the dynamic reloads.
    $Page:Table = New-UDTable -Data $TableData -Paging -ShowSelection
    $Page:Table
} 

New-UDButton -Text 'Refresh Table' -OnClick {
    Sync-UDElement -Id 'table'
}

New-UDButton -Text 'Get Data' -OnClick {
    Show-UDToast (Get-UDElement -Id $Page:Table.Id | ConvertTo-Json)
}
```

### LoadData Parameter

If you use the `-LoadData` parameter, you can sync the table directly. This has the benefit of maintaining the table state, such as the page and filtering, after the refresh.

```powershell
New-UDButton -Text 'Table1' -OnClick { Sync-UDElement -Id 'Table1' }

$Columns = @(
    New-UDTableColumn -Property Name -Title "Name" -ShowFilter -Render { $EventData.Name }
    New-UDTableColumn -Property Value -Title "Value" -ShowFilter
)

New-UDTable -Columns $Columns -LoadData {
    $TableData = 1..1000 | ForEach-Object {
        @{
            Name = "Record-$_"
            Value = $_ 
        }
    }
    
    foreach($Filter in $EventData.Filters)
    {
        $TableData = $TableData | Where-Object -Property $Filter.Id -Match -Value $Filter.Value
    }

    $TotalCount = $TableData.Count 

    if (-not [string]::IsNullOrEmpty($EventData.OrderBy))
    {
        $Descending = $EventData.OrderDirection -ne 'asc'
        $TableData = $TableData | Sort-Object -Property $EventData.orderBy -Descending:$Descending
    }
    
    $TableData = $TableData | Select-Object -First $EventData.PageSize -Skip ($EventData.Page * $EventData.PageSize)

    $TableData | Out-UDTableData -Page $EventData.Page -TotalCount $TotalCount -Properties $EventData.Properties 
} -ShowFilter -ShowSort -ShowPagination  -Id 'Table1'
```

## Show Refresh Button

You can use the `-ShowRefresh` parameter to provide a refresh button for server-side tables.

```powershell
$Columns = @(
    New-UDTableColumn -Property Dessert -Title "A Dessert"
    New-UDTableColumn -Property Calories -Title Calories 
    New-UDTableColumn -Property Fat -Title Fat 
    New-UDTableColumn -Property Carbs -Title Carbs 
    New-UDTableColumn -Property Protein -Title Protein 
)

New-UDTable -ShowRefresh -Columns $Columns -LoadData {
    $Query = $Body | ConvertFrom-Json

    <# Query will contain
        filters: []
        orderBy: undefined
        orderDirection: ""
        page: 0
        pageSize: 5
        properties: (5) ["dessert", "calories", "fat", "carbs", "protein"]
        search: ""
        totalCount: 0
    #>

    @(
        @{Dessert = 'Frozen yoghurt'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Ice cream sandwich'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Eclair'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Cupcake'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Gingerbread'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
    ) | Out-UDTableData -Page 0 -TotalCount 5 -Properties $Query.Properties 
}
```

## Alternating Row Colors

You can use a theme to create a table with alternating row colors.

<figure><img src="../../../.gitbook/assets/image (521).png" alt=""><figcaption></figcaption></figure>

```powershell
$Theme = @{
    overrides = @{
        MuiTableRow = @{
            root = @{
                '&:nth-of-type(odd)' = @{
                    backgroundColor = "rgba(0,0,0,0.04)"
                }
            }
            head = @{
                backgroundColor = "rgb(255,255,255) !important"
            }
        }
    }
}

New-UDDashboard -Content {
$TableData = 1..10 | % { [PSCustomObject]@{ Item = $_}}
  New-UDTable -ShowPagination -PageSize 10 -PageSizeOptions @(10, 10) -DisablePageSizeAll -Columns @(
        New-UDTableColumn -Property 'Item' -Title 'Item' -Width 180 -Truncate
    ) -Data $TableData -Dense -ShowSearch
} -Theme $Theme
```

## API

* [New-UDTable](../../../cmdlets/New-UDTable.txt)
* [New-UDTableColumn](../../../cmdlets/New-UDTableColumn.txt)
* [Out-UDTableColumn](../../../cmdlets/Out-UDTableData.txt)
* [New-UDTableTextOption](../../../cmdlets/New-UDTableTextOption.txt)
