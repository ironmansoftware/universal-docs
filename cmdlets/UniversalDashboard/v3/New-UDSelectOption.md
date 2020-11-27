---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDSelectOption

## SYNOPSIS
Creates a new select option.

## SYNTAX

```
New-UDSelectOption [-Name] <String> [-Value] <String> [<CommonParameters>]
```

## DESCRIPTION
Creates a new select option.
This cmdlet is to be used with New-UDSelect.
Pass the result of this cmdlet to the -Option parameter to create a new select group.

## EXAMPLES

### EXAMPLE 1
```
Creates a new select with three options.
```

New-UDSelect -Label '1-3' -Id 'select' -Option {
    New-UDSelectOption -Name "One" -Value 1
    New-UDSelectOption -Name "Two" -Value 2
    New-UDSelectOption -Name "Three" -Value 3
} -DefaultValue 2 -OnChange { 
    $EventData = $Body | ConvertFrom-Json
    Set-TestData $EventData 
}

## PARAMETERS

### -Name
The name of the select option.
This will be shown in the select.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Value
Thevalue of the select option.
This will be passed back to New-UDForm -OnSubmit or the $EventData for -OnChange on New-UDSelect.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
