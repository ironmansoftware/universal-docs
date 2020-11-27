---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDTable

## SYNOPSIS
Creates a table.

## SYNTAX

### Static
```
New-UDTable [-Id <String>] [-Title <String>] -Data <Object[]> [-Columns <Hashtable[]>]
 [-OnRowSelection <Endpoint>] [-ShowSort] [-ShowFilter] [-ShowSearch] [-Dense] [-ShowExport] [-StickyHeader]
 [-PageSize <Int32>] [-PageSizeOptions <Int32[]>] [-ShowSelection] [-ShowPagination] [-Padding <String>]
 [-Size <String>] [<CommonParameters>]
```

### Dynamic
```
New-UDTable [-Id <String>] [-Title <String>] -LoadData <Endpoint> -Columns <Hashtable[]>
 [-OnRowSelection <Endpoint>] [-ShowSort] [-ShowFilter] [-ShowSearch] [-Dense] [-ShowExport] [-StickyHeader]
 [-PageSize <Int32>] [-PageSizeOptions <Int32[]>] [-ShowSelection] [-ShowPagination] [-Padding <String>]
 [-Size <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a table.
Tables are used to show both static and dyanmic data.
You can define columns and data to show within the table.
The columns can be used to render custom components based on row data.
You can also enable paging, filtering, sorting and even server-side processing.

## EXAMPLES

### EXAMPLE 1
```
Creates a static table whether the columns of the table are the properties of the data specified.
```

$Data = @(
    @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
) 

New-UDTable -Id 'defaultTable' -Data $Data

### EXAMPLE 2
```
Creates a table where there are custom columns defined for that table.
```

$Columns = @(
    New-UDTableColumn -Property Dessert -Title "A Dessert"
    New-UDTableColumn -Property Calories -Title Calories 
    New-UDTableColumn -Property Fat -Title Fat 
    New-UDTableColumn -Property Carbs -Title Carbs 
    New-UDTableColumn -Property Protein -Title Protein 
)

New-UDTable -Id 'customColumnsTable' -Data $Data -Columns $Columns

### EXAMPLE 3
```
Creates a table where the table has custom rendering for one of the columns and an export button.
```

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

New-UDTable -Id 'customColumnsTableRender' -Data $Data -Columns $Columns -Sort -Export

### EXAMPLE 4
```
Creates a table within a New-UDDynamic that refreshes automatically on an interval.
```

New-UDDynamic -Content {
    $DynamicData = @(
        @{Dessert = 'Frozen yoghurt'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Ice cream sandwich'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Eclair'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Cupcake'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Gingerbread'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
    ) 

    New-UDTable -Id 'dynamicTable' -Data $DynamicData
} -AutoRefresh -AutoRefreshInterval 2

### EXAMPLE 5
```
Creates a table that uses the LoadData script block to load data dynamically.
```

New-UDTable -Id 'loadDataTable' -Columns $Columns -LoadData {
$Query = $Body | ConvertFrom-Json

@(
    @{Dessert = 'Frozen yoghurt'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Ice cream sandwich'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Eclair'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Cupcake'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
    @{Dessert = 'Gingerbread'; Calories = (Get-Random); Fat = 6.0; Carbs = 24; Protein = 4.0}
) | Out-UDTableData -Page 0 -TotalCount 5 -Properties $Query.Properties

## PARAMETERS

### -Id
The ID of the component.
It defaults to a random GUID.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: [Guid]::NewGuid().ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Title
The title to show at the top of the table's card.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Data
The data to put into the table.

```yaml
Type: Object[]
Parameter Sets: Static
Aliases:

Required: True
Position: Named
Default value: @()
Accept pipeline input: False
Accept wildcard characters: False
```

### -LoadData
When using dynamic tables, this script block is called.
The $Body parameter will contain a hashtable the following options: 

filters: @()
orderBy: string
orderDirection: string
page: int
pageSize: int
properties: @()
search: string
totalCount: int

You can use these values to perform server-side processing, like SQL queries, to improve the performance of large grids. 

After processing the data with these values, output the data via Out-UDTableData.

```yaml
Type: Endpoint
Parameter Sets: Dynamic
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Columns
Defines the columns to show within the table.
Use New-UDTableColumn to define these columns.
If this parameter isn't specified, the properties of the data that you pass in will become the columns.

```yaml
Type: Hashtable[]
Parameter Sets: Static
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

```yaml
Type: Hashtable[]
Parameter Sets: Dynamic
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnRowSelection
{{ Fill OnRowSelection Description }}

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ShowSort
{{ Fill ShowSort Description }}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: Sort

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -ShowFilter
{{ Fill ShowFilter Description }}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: Filter

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -ShowSearch
{{ Fill ShowSearch Description }}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: Search

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Dense
{{ Fill Dense Description }}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -ShowExport
{{ Fill ShowExport Description }}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: Export

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -StickyHeader
{{ Fill StickyHeader Description }}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -PageSize
{{ Fill PageSize Description }}

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: 5
Accept pipeline input: False
Accept wildcard characters: False
```

### -PageSizeOptions
{{ Fill PageSizeOptions Description }}

```yaml
Type: Int32[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: @()
Accept pipeline input: False
Accept wildcard characters: False
```

### -ShowSelection
{{ Fill ShowSelection Description }}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: Select

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -ShowPagination
{{ Fill ShowPagination Description }}

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: Paging

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Padding
{{ Fill Padding Description }}

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: Default
Accept pipeline input: False
Accept wildcard characters: False
```

### -Size
{{ Fill Size Description }}

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: Medium
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES
General notes

## RELATED LINKS
