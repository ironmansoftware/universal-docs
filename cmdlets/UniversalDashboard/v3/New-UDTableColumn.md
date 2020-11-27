---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDTableColumn

## SYNOPSIS
Defines a table column.

## SYNTAX

```
New-UDTableColumn [[-Id] <String>] [-Property] <String> [[-Title] <String>] [[-Render] <ScriptBlock>]
 [-ShowSort] [-ShowFilter] [[-FilterType] <String>] [[-Style] <Hashtable>] [[-Width] <Int32>]
 [-IncludeInSearch] [-IncludeInExport] [-DefaultSortColumn] [[-Align] <String>] [<CommonParameters>]
```

## DESCRIPTION
Defines a table column.
Use this cmdlet in conjunction with New-UDTable's -Column property.
Table columns can be used to control many aspects of the columns within a table.

## EXAMPLES

### EXAMPLE 1
```
See New-UDTable for examples.
```

## PARAMETERS

### -Id
The ID of the component.
It defaults to a random GUID.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: [Guid]::NewGuid().ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Property
The property to select from the data.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Title
The title of the column to show at the top of the table.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Render
How to render this table.
Use this parameter instead of property to render custom content within a column.
The $Body variable will contain the current row being rendered.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
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

### -FilterType
{{ Fill FilterType Description }}

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 5
Default value: Text
Accept pipeline input: False
Accept wildcard characters: False
```

### -Style
{{ Fill Style Description }}

```yaml
Type: Hashtable
Parameter Sets: (All)
Aliases:

Required: False
Position: 6
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Width
{{ Fill Width Description }}

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: 7
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -IncludeInSearch
{{ Fill IncludeInSearch Description }}

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

### -IncludeInExport
{{ Fill IncludeInExport Description }}

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

### -DefaultSortColumn
{{ Fill DefaultSortColumn Description }}

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

### -Align
{{ Fill Align Description }}

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 8
Default value: Inherit
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
