---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDGrid

## SYNOPSIS
Creates a grid to layout components.

## SYNTAX

### Item
```
New-UDGrid [-Id <String>] [-ExtraSmallSize <Int32>] [-SmallSize <Int32>] [-MediumSize <Int32>]
 [-LargeSize <Int32>] [-ExtraLargeSize <Int32>] [-Item] [-Children <ScriptBlock>] [<CommonParameters>]
```

### Container
```
New-UDGrid [-Id <String>] [-Container] [-Spacing <Int32>] [-Children <ScriptBlock>] [<CommonParameters>]
```

## DESCRIPTION
Creates a grid to layout components.
The grid is a 24-point grid system that can adapt based on the size of the screen that is showing the controls.

## EXAMPLES

### EXAMPLE 1
```
An example
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
Position: Named
Default value: [Guid]::NewGuid().ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### -ExtraSmallSize
The size (1-24) for extra small devices.

```yaml
Type: Int32
Parameter Sets: Item
Aliases: Size

Required: False
Position: Named
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -SmallSize
The size (1-24) for small devices.

```yaml
Type: Int32
Parameter Sets: Item
Aliases:

Required: False
Position: Named
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -MediumSize
The size (1-24) for medium devices.

```yaml
Type: Int32
Parameter Sets: Item
Aliases:

Required: False
Position: Named
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -LargeSize
The size (1-24) for large devices.

```yaml
Type: Int32
Parameter Sets: Item
Aliases:

Required: False
Position: Named
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -ExtraLargeSize
The size (1-24) for extra large devices.

```yaml
Type: Int32
Parameter Sets: Item
Aliases:

Required: False
Position: Named
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -Container
Whether this is a container.
A container can be best described as a row.

```yaml
Type: SwitchParameter
Parameter Sets: Container
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Spacing
Spacing between the items.

```yaml
Type: Int32
Parameter Sets: Container
Aliases:

Required: False
Position: Named
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -Item
Whether this is an item in a container.

```yaml
Type: SwitchParameter
Parameter Sets: Item
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Children
Components included in this grid item.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases: Content

Required: False
Position: Named
Default value: None
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
