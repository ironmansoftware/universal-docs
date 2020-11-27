---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# Debug-PSUDashboard

## SYNOPSIS
Provides a utility function for debugging scripts running PowerShell Universal Dashboard.

## SYNTAX

```
Debug-PSUDashboard [<CommonParameters>]
```

## DESCRIPTION
Provides a utility function for debugging scripts running PowerShell Universal Dashboard.
This cmdlet integrates with the VS Code PowerShell Universal extension to automatically connect the debugger to endpoints running in UD.

## EXAMPLES

### EXAMPLE 1
```
Creates an element that invokes the Debug-PSUDashboard cmdlet.
```

New-UDElement -Tag div -Endpoint {
    Debug-PSUDashboard
}

## PARAMETERS

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
