---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# Out-UDTableData

## SYNOPSIS
Formats data to be output from New-UDTable's -LoadData script block.

## SYNTAX

```
Out-UDTableData [-Data] <Object> [-Page] <Int32> [-TotalCount] <Int32> [-Properties] <String[]>
 [<CommonParameters>]
```

## DESCRIPTION
Formats data to be output from New-UDTable's -LoadData script block.

## EXAMPLES

### EXAMPLE 1
```
See New-UDTable for examples.
```

## PARAMETERS

### -Data
The data to return from LoadData.

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Page
The current page we are on within the table.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: True
Position: 2
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -TotalCount
The total count of items within the data set.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: True
Position: 3
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -Properties
The properties that are currently passed from the table.
You can return the array from the $EventData.Properties array.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: Property

Required: True
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
