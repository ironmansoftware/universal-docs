---
external help file: UniversalDashboard.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Remove-UDEndpoint

## SYNOPSIS
Removes a scheduled endpoint.

## SYNTAX

```
Remove-UDEndpoint -Id <String> [<CommonParameters>]
```

## DESCRIPTION
Removes a scheduled endpoint.

## EXAMPLES

### Example 1
```powershell
$Schedule = New-UDEndpointSchedule 10 -Second
New-UDEndpoint -Schedule $Schedule -Endpoint {
    $Cache:Processes = Get-Process
} -Id 'MySchedule' 

Remove-UDEndpoint -Id 'MySchedule'
```

Removes the endpoint 'MySchedule'

## PARAMETERS

### -Id
The Id of the endpoint to remove. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
