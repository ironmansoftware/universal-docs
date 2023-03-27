---
external help file: UniversalDashboard.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-UDEndpoint

## SYNOPSIS
Creates a scheduled endpoint with a dashboard. 

## SYNTAX

### Generic (Default)
```
New-UDEndpoint -Endpoint <ScriptBlock> [-ArgumentList <Object[]>] [-Id <String>] [-Role <String[]>]
 [<CommonParameters>]
```

### Scheduled
```
New-UDEndpoint -Endpoint <ScriptBlock> [-ArgumentList <Object[]>] [-Id <String>] -Schedule <EndpointSchedule>
 [-Role <String[]>] [<CommonParameters>]
```

## DESCRIPTION
Creates a scheduled endpoint with a dashboard. 

## EXAMPLES

### Example 1
```powershell
$Schedule = New-UDEndpointSchedule 10 -Second
New-UDEndpoint -Schedule $Schedule -Endpoint {
    $Cache:Processes = Get-Process
}
```

Caches the local machines processes every 10 seconds. 

## PARAMETERS

### -ArgumentList
Not required. 

```yaml
Type: Object[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Endpoint
The endpoint to run on the schedule. 

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id
The ID of the endpoint. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Role
Not used. 

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Schedule
The schedule to run for the endpoint. Use New-UDEndpointSchedule to create a schedule object. 

```yaml
Type: EndpointSchedule
Parameter Sets: Scheduled
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
