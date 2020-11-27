---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDSlider

## SYNOPSIS
A slider component.

## SYNTAX

```
New-UDSlider [[-Id] <String>] [[-Value] <Int32[]>] [[-Minimum] <Int32>] [[-Maximum] <Int32>] [-Disabled]
 [-Marks] [[-OnChange] <Endpoint>] [[-Orientation] <String>] [[-Step] <Int32>] [[-ValueLabelDisplay] <String>]
 [<CommonParameters>]
```

## DESCRIPTION
A slider component.
Sliders can be used to define values within a range or selecting a range of values.
You can use this component with New-UDForm.

## EXAMPLES

### EXAMPLE 1
```
An example
```

New-UDSlider

## PARAMETERS

### -Id
The ID of this component.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: ([Guid]::NewGuid())
Accept pipeline input: False
Accept wildcard characters: False
```

### -Value
The value of the slider.

```yaml
Type: Int32[]
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -Minimum
The minimum value of the slider.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -Maximum
The maximum value of the slider.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: 100
Accept pipeline input: False
Accept wildcard characters: False
```

### -Disabled
Whether the slider is disabled.

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

### -Marks
Whether to display marks on the slider.

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

### -OnChange
A script block that is invoked when the slider value changes.
You can access the slider value within the script block by referencing the $EventData variable.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 5
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Orientation
The orientation of the slider.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 6
Default value: Horizontal
Accept pipeline input: False
Accept wildcard characters: False
```

### -Step
Step size of the slider.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: 7
Default value: 1
Accept pipeline input: False
Accept wildcard characters: False
```

### -ValueLabelDisplay
Whether to display value labels.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 8
Default value: Auto
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
