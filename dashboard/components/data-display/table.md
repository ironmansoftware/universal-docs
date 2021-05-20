---
description: Table component for Universal Dashboard
---

# Table

Tables display sets of data. They can be fully customized.

Tables display information in a way that’s easy to scan, so that users can look for patterns and insights. They can be embedded in primary content, such as cards.

## Simple Table

![](../../../.gitbook/assets/image%20%2858%29.png)

A simple example with no frills. Table columns are defined from the data.

```text
$Data = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

New-UDTable -Data $Data
```

## Table with Custom Columns

![](../../../.gitbook/assets/image%20%2853%29.png)

Define custom columns for your table.

```text
$Data = @(
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

New-UDTable -Id 'customColumnsTable' -Data $Data -Columns $Columns
```

## Table with Custom Column Rendering

![](../../../.gitbook/assets/image%20%2860%29.png)

Define column rendering. Sorting and exporting still work for the table.

```text
$Data = @(
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

New-UDTable -Data $Data -Columns $Columns -Sort -Export
```

## Table Column Width

Column width can be defined using the `-Width` parameter. You can also decide to truncate columns that extend past that width.

```text
$Data = @(
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

New-UDTable -Data $Data -Columns $Columns -Sort
```

## Filters

You can configure custom filters per column. The table supports `text`, `select`, `fuzzy` , `slider`, `range`, `date` , `number`, and `autocomplete` filters.

```text
$Data = @(
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

New-UDTable -Id 'customColumnsTable' -Data $Data -Columns $Columns -ShowFilter
```

![](../../../.gitbook/assets/image%20%28221%29.png)

## Table with server-side processing

For a full example of server-side processing, [see this blog post](https://blog.ironmansoftware.com/universal-dashboard-server-side-table/).

![](../../../.gitbook/assets/image%20%2854%29.png)

Process data on the server so you can perform paging, filtering, sorting and searching in systems like SQL.

```text
$Columns = @(
    New-UDTableColumn -Property Dessert -Title "A Dessert"
    New-UDTableColumn -Property Calories -Title Calories 
    New-UDTableColumn -Property Fat -Title Fat 
    New-UDTableColumn -Property Carbs -Title Carbs 
    New-UDTableColumn -Property Protein -Title Protein 
)

New-UDTable -Columns $Columns -LoadData {
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

## Selection

Tables support selection of rows. You can create an event handler for the `OnRowSelected` parameter to receive when a new row is selected or unselected or you can use `Get-UDElement` to retrieve the current set of selected rows.

The following example creates a table with row selection enabled. A toast is show when clicking the row or when clicking the GET Rows button.

```text
$Data = try { get-service -ea Stop | select Name,@{n = "Status";e={ $_.Status.ToString()}},@{n = "StartupType";e={ $_.StartupType.ToString()}},@{n = "StartType";e={ $_.StartType.ToString()}} } catch {}
$Columns = @(
    New-UDTableColumn -Property Name -Title "Service Name" -ShowSort -IncludeInExport -IncludeInSearch -ShowFilter -FilterType text
    New-UDTableColumn -Property Status -Title Status -ShowSort -DefaultSortColumn -IncludeInExport -IncludeInSearch -ShowFilter -FilterType select 
    New-UDTableColumn -Property StartupType -Title StartupType -IncludeInExport -ShowFilter -FilterType select
    New-UDTableColumn -Property StartType -Title StartType -IncludeInExport -ShowFilter -FilterType select 
)
New-UDTable -Id 'service_table' -Data $Data -Columns $Columns -Title 'Services' -ShowSearch -ShowPagination -ShowSelection -Dense -OnRowSelection {
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

```text
@{
   Id = 0
   Name = 'AESMService',
   Status = 'Running'
   StartupType = 'AutomaticDelayedStart'
   StartType = 'Automation'
   selected = $true
}
```

## Exporting

Tables support exporting the data within the table. You can export as CSV, XLSX, JSON or PDF. You can define which columns to include in an export and choose to export just the current page or all the data within the table.

```text
$Data = try { get-service -ea Stop | select Name,@{n = "Status";e={ $_.Status.ToString()}},@{n = "StartupType";e={ $_.StartupType.ToString()}},@{n = "StartType";e={ $_.StartType.ToString()}} } catch {}
$Columns = @(
    New-UDTableColumn -Property Name -Title "Service Name" -IncludeInExport
    New-UDTableColumn -Property Status -Title Status 
    New-UDTableColumn -Property StartupType
    New-UDTableColumn -Property StartType -IncludeInExport
)
New-UDTable -Id 'service_table' -Data $Data -Columns $Columns -Title 'Services' -ShowSearch -ShowPagination -Dense -Export
```

![](../../../.gitbook/assets/image%20%28176%29.png)

## Server-Side Exporting

You can control the export functionality with a PowerShell script block. This is useful when exporting from server-side sources like SQL server tables.

In this example, I have a SQL table that contains podcasts. When exporting, you will receive information about the current state of the table to allow you to customize what data is exported.

```text
New-UDDashboard -Title "Hello, World!" -Content {
    New-UDTable -Title 'Shows' -LoadData {
        $TableData = ConvertFrom-Json $Body

        $OrderBy = $TableData.orderBy.field
        if ($OrderBy -eq $null)
        {
            $OrderBy = "name"
        }

        $OrderDirection = $TableData.OrderDirection
        if ($OrderDirection -eq $null)
        {
            $OrderDirection = 'asc'
        }

        $Where = ""
        if ($TableData.Filters) 
        {
            $Where = "WHERE "

            foreach($filter in $TableData.Filters)
            {
                $Where += $filter.column.field + " LIKE '%" + $filter.value + "%' AND "
            }

            $Where += " 1 = 1"
        }

        $PageSize = $TableData.PageSize 
        # Calculate the number of rows to skip
        $Offset = $TableData.Page * $PageSize
        $Count = Invoke-DbaQuery -SqlInstance localhost\MSSQLSERVER -Database 'podcasts' -Query "SELECT COUNT(*) as count FROM shows $Where"

        $Data = Invoke-DbaQuery -SqlInstance localhost\MSSQLSERVER -Database 'podcasts' -Query "SELECT * FROM shows $Where ORDER BY $orderBy $orderdirection OFFSET $Offset ROWS FETCH NEXT $PageSize ROWS ONLY" | ForEach-Object {
            @{ 
                name = $_.name 
                host = $_.host
            }
        } 
        $Data | Out-UDTableData -Page $TableData.page -TotalCount $Count.Count -Properties $TableData.properties
    } -Columns @(
        New-UDTableColumn -Property 'name' -Sort -Filter -Export
        New-UDTableColumn -Property 'host' -Sort -Filter -Export
    ) -Sort -Filter -Export -OnExport {
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

        Invoke-DbaQuery -SqlInstance localhost\MSSQLSERVER -Database 'podcasts' -Query "SELECT * FROM shows" | ForEach-Object {
            @{ 
                name = $_.name 
                host = $_.host
            }
        } 
    }
}
```

## Customizing Export Options

You can decide which export options to present to your users using the `-ExportOption` cmdlet. The following example would only show the CSV export option.

```text
$Data = try { get-service -ea Stop | select Name,@{n = "Status";e={ $_.Status.ToString()}},@{n = "StartupType";e={ $_.StartupType.ToString()}},@{n = "StartType";e={ $_.StartType.ToString()}} } catch {}
$Columns = @(
    New-UDTableColumn -Property Name -Title "Service Name" -IncludeInExport
    New-UDTableColumn -Property Status -Title Status 
    New-UDTableColumn -Property StartupType
    New-UDTableColumn -Property StartType -IncludeInExport
)
New-UDTable -Id 'service_table' -Data $Data -Columns $Columns -Title 'Services' -ShowSearch -ShowPagination -Dense -Export -ExportOption "csv"
```

## Customizing Labels

You can use the `-TextOption` parameter along with the `New-UDTableTextOption` cmdlet to set text fields within the table.

```text
$Data = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

$Option = New-UDTableTextOption -Search "Search all these records"

New-UDTable -Data $Data -TextOption $Option -ShowSearch
```

## Refresh with a button

You can externally refresh a table by putting the table within a dynamic region and using `Sync-UDElement`.

This example creates a button to refresh the table.

```text
New-UDDynamic -Id 'table' -Content {
    $Data = Get-Service
    New-UDTable -Data $Data -Paging
} -LoadingComponent {
    "Loading"
}

New-UDButton -Text 'Refresh Table' -OnClick {
    Sync-UDElement -Id 'table'
}
```

**New-UDTable**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Title | String | The title to show at the top of the table's card. | false |
| Data | Object\[\] | The data to put into the table. | true |
| LoadData | Endpoint | When using dynamic tables, this script block is called. The $Body parameter will contain a hashtable the following options: filters: @\(\) orderBy: string orderDirection: string page: int pageSize: int properties: @\(\) search: string totalCount: int You can use these values to perform server-side processing, like SQL queries, to improve the performance of large grids. After processing the data with these values, output the data via Out-UDTableData. | true |
| Columns | Hashtable\[\] | Defines the columns to show within the table. Use New-UDTableColumn to define these columns. If this parameter isn't specified, the properties of the data that you pass in will become the columns. | false |
| Sort | SwitchParameter | Whether sorting is enabled in the table. | false |
| Filter | SwitchParameter | Whether filtering is enabled in the table. | false |
| Search | SwitchParameter | Whether search is enabled in the table. | false |
| Export | SwitchParameter | Whether exporting is enabled within the table. | false |
| PageSize | int | Number of items to show in a page by default. Defaults to 5. | false |
| PageSizeOptions | int\[\] | Page size options to show in the selector. Defaults to @\(5, 10, 20\) _\*\*_ | false |
| Dense | SwitchParameter | Enables dense padding. | false |
| DefaultSort Direction | string | Sets the default sort direction for the table.  | false |
| HideToggleAllRowsSelected | SwitchParameter | Disables the toggle all rows when using selection | false |
| DisableMultiSelect | SwitchParameter | Disables multiple selections | false |

