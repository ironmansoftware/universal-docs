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
        $Item = $Body | ConvertFrom-Json 
        New-UDButton -Id "btn$($Item.Dessert)" -Text "Click for Dessert!" -OnClick { Show-UDToast -Message $Item.Dessert } 
    }
    New-UDTableColumn -Property Calories -Title Calories 
    New-UDTableColumn -Property Fat -Title Fat 
    New-UDTableColumn -Property Carbs -Title Carbs 
    New-UDTableColumn -Property Protein -Title Protein 
)

New-UDTable -Data $Data -Columns $Columns -Sort -Export
```

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
| PageSize   | int | Number of items to show in a page by default \(prerelease\) | 5 |
| PageSizeOptions | int\[\] | Page size options to show in the selector. | @\(5, 10, 20\) |

