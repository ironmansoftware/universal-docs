---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDTooltip

## SYNOPSIS
A tooltip component.

## SYNTAX

```
New-UDTooltip [[-Id] <String>] [[-Place] <String>] [[-Type] <String>] [[-Effect] <String>]
 [-TooltipContent] <ScriptBlock> [-Content] <ScriptBlock> [<CommonParameters>]
```

## DESCRIPTION
A tooltip component.
Tooltips can be placed over an other component to display a popup when the user hovers over the nested component.

## EXAMPLES

### EXAMPLE 1
```
A simple tooltip.
```

New-UDTooltip -Content {
    New-UDTypography -Text 'Hover me'
} -TooltipContent {
    New-UDTypography -Text 'I'm a tooltip'
}

## PARAMETERS

### -Id
The ID of this component.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: [Guid]::NewGuid()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Place
Where to place the tooltip.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: Top
Accept pipeline input: False
Accept wildcard characters: False
```

### -Type
The type of tooltip.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: Dark
Accept pipeline input: False
Accept wildcard characters: False
```

### -Effect
An effect to apply to the tooltip.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -TooltipContent
Content to display within the tooltip.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: True
Position: 5
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Content
Content that activates the tooltip when hovered.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: True
Position: 6
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
