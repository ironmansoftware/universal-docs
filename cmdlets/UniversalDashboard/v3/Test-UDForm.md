---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# Test-UDForm

## SYNOPSIS
Invokes validation for a form.

## SYNTAX

```
Test-UDForm [-Id] <String> [<CommonParameters>]
```

## DESCRIPTION
Invokes validation for a form.

## EXAMPLES

### EXAMPLE 1
```
New-UDButton -Text 'Validate' -OnClick {
    Test-UDForm -Id 'myForm'
}
```

## PARAMETERS

### -Id
Id of the form to invoke validation for.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
