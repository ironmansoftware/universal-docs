---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDValidationResult

## SYNOPSIS
Creates a new validation result.

## SYNTAX

```
New-UDValidationResult [-Valid] [[-ValidationError] <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new validation result.
This cmdlet should return its value from the OnValidate script block parameter on New-UDForm or New-UDStepper.

## EXAMPLES

### EXAMPLE 1
```
An example
```

## PARAMETERS

### -Valid
Whether the status is considered valid.

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

### -ValidationError
An error to display if the is not valid.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: Form is invalid.
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
