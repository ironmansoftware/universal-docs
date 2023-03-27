---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Write-PSUError

## SYNOPSIS
Writes an error to the error stream in PSU jobs.

## SYNTAX

```
Write-PSUError -ErrorRecord <ErrorRecord> [<CommonParameters>]
```

## DESCRIPTION
Writes an error to the error stream in PSU jobs.

## EXAMPLES

### Example 1
```powershell
try {
    throw "Error"
} catch {
    Write-PSUError $_
}
```

Throws an exception but does not fail the job. The error will be displayed in the PSU error log. 

## PARAMETERS

### -ErrorRecord
The error record to display in the log. 

```yaml
Type: ErrorRecord
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.Management.Automation.ErrorRecord

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
