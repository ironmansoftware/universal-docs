---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDProgress

## SYNOPSIS
Creates a progress dialog.

## SYNTAX

### indeterminate (Default)
```
New-UDProgress [-Id <String>] [-BackgroundColor <DashboardColor>] [-ProgressColor <DashboardColor>]
 [<CommonParameters>]
```

### determinate
```
New-UDProgress [-Id <String>] [-PercentComplete <Object>] [-BackgroundColor <DashboardColor>]
 [-ProgressColor <DashboardColor>] [<CommonParameters>]
```

### circular
```
New-UDProgress [-Id <String>] [-Circular] [-Color <String>] [-Size <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a progress dialog.
Progress dialogs can show both determinate and indeterminate progress.
They can also be circular or linear.

## EXAMPLES

### EXAMPLE 1
```
Creates a progress bar at 75%.
```

New-UDProgress -PercentComplete 75

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

### -PercentComplete
The percent complete for the progress.

```yaml
Type: Object
Parameter Sets: determinate
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -BackgroundColor
The background color.

```yaml
Type: DashboardColor
Parameter Sets: indeterminate, determinate
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ProgressColor
The progress bar color.

```yaml
Type: DashboardColor
Parameter Sets: indeterminate, determinate
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Circular
Whether the progress is circular.

```yaml
Type: SwitchParameter
Parameter Sets: circular
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Color
The color of the progress.

```yaml
Type: String
Parameter Sets: circular
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Size
The size of the progress.

```yaml
Type: String
Parameter Sets: circular
Aliases:

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

## RELATED LINKS
