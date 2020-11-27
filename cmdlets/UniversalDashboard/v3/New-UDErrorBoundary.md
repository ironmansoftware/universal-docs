---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDErrorBoundary

## SYNOPSIS
Defines a new error boundary around a section of code.

## SYNTAX

```
New-UDErrorBoundary [-Content] <ScriptBlock> [<CommonParameters>]
```

## DESCRIPTION
Defines a new error boundary around a section of code.
Error boundaries are used to trap errors and display them on the page.

## EXAMPLES

### EXAMPLE 1
```
Defines an error boundary that traps the exception that is thrown and displays it on the page.
```

New-UDErrorBoundary -Content {
    throw 'This is an error'
}

## PARAMETERS

### -Content
The content to trap in an error boundary.

```yaml
Type: ScriptBlock
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
