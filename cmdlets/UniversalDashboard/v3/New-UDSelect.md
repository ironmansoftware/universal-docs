---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDSelect

## SYNOPSIS
Creates a new select.

## SYNTAX

```
New-UDSelect [[-Id] <String>] [[-Option] <ScriptBlock>] [[-Label] <String>] [[-OnChange] <Endpoint>]
 [[-DefaultValue] <String>] [-Disabled] [-Multiple] [<CommonParameters>]
```

## DESCRIPTION
Creates a new select.
Selects can have multiple options and option groups.
Selects can also be multi-select.

## EXAMPLES

### EXAMPLE 1
```
Creates a new select with 3 options and shows a toast when one is selected.
```

New-UDSelect -Label '1-3' -Id 'select' -Option {
    New-UDSelectOption -Name "One" -Value 1
    New-UDSelectOption -Name "Two" -Value 2
    New-UDSelectOption -Name "Three" -Value 3
} -DefaultValue 2 -OnChange { 
    Show-UDToast -Mesage $EventData 
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

### -Option
Options to include in this select.
This can be either New-UDSelectOption or New-UDSelectGroup.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Label
The label to show with the select.

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

### -OnChange
A script block that is executed when the script changes.
$EventData will be an array of the selected values.

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

### -DefaultValue
The default selected value.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 5
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Disabled
Whether this select is disabled.

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

### -Multiple
Whether you can select multiple values.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
