---
description: Data grid component for Universal Dashboard.
---

# Data Grid

The `UDDataGrid` component is an advanced version of the table that is useful for displaying large amounts of data. It supports many of the same features as the table but also provides complex filtering, row virtualization, multi-column sort and more.&#x20;

## Simple Data Grid

![](<../../../../.gitbook/assets/image (5).png>)

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
    @{ field = "name"; 
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

![](<../../../../.gitbook/assets/image (2).png>)

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
|          |                                  |           |
