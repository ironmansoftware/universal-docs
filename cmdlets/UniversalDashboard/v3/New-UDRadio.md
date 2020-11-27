---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDRadio

## SYNOPSIS
Creates a radio.

## SYNTAX

```
New-UDRadio [[-Id] <String>] [[-Label] <String>] [-Disabled] [[-Value] <String>] [[-LabelPlacement] <String>]
 [<CommonParameters>]
```

## DESCRIPTION
Creates a radio.
Radios should be included within a New-UDRadioGroup.

## EXAMPLES

### EXAMPLE 1
```
Creates a radio group that shows a toast message when a radio is selected.
```

New-UDRadioGroup -Label 'group' -Id 'onChangeRadio' -Children {
    New-UDRadio -Value 'Adam' -Label 'Adam'  -Id 'adamOnChange'
    New-UDRadio -Value 'Alon' -Label 'Alon' -Id 'alonOnChange'
    New-UDRadio -Value 'Lee' -Label 'Lee' -Id 'leeOnChange'
} -OnChange { 
    Show-UDToast $EventData 
}

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
Default value: ([Guid]::NewGuid())
Accept pipeline input: False
Accept wildcard characters: False
```

### -Label
The label to show next to the radio.

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

### -Disabled
Whether the radio is disabled.

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

### -Value
The value of the radio.

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

### -LabelPlacement
The position to place the label in relation to the radio.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: End
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
