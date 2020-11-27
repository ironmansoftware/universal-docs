---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDDatePicker

## SYNOPSIS
Creates a new date picker.

## SYNTAX

```
New-UDDatePicker [[-Id] <String>] [[-Label] <String>] [[-Variant] <String>] [-DisableToolbar]
 [[-OnChange] <Endpoint>] [[-Format] <String>] [[-Value] <DateTime>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new date picker.
Date pickers can be used stand alone or within New-UDForm.

## EXAMPLES

### EXAMPLE 1
```
Creates a new date picker with the default date value.
```

New-UDDatePicker -Id 'dateDateDefault' -Value '1-2-2020'

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

### -Label
The label to show next to the date picker.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Variant
The theme variant to apply to the date picker.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: Inline
Accept pipeline input: False
Accept wildcard characters: False
```

### -DisableToolbar
Disables the date picker toolbar.

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
A script block to call with the selected date.
The $EventData variable will be the date selected.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Format
The format of the date when it is selected.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 5
Default value: MM/dd/yyyy
Accept pipeline input: False
Accept wildcard characters: False
```

### -Value
The current value of the date picker.

```yaml
Type: DateTime
Parameter Sets: (All)
Aliases:

Required: False
Position: 6
Default value: (Get-Date).Date
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
