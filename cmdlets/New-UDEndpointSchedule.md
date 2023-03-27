---
external help file: UniversalDashboard.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-UDEndpointSchedule

## SYNOPSIS
Creates a schedule for New-UDEndpoint. 

## SYNTAX

### EverySecond
```
New-UDEndpointSchedule -Every <Int32> [-Repeat <Int32>] [-Consecutive] [-Second] [<CommonParameters>]
```

### EveryMinute
```
New-UDEndpointSchedule -Every <Int32> [-Repeat <Int32>] [-Consecutive] [-Minute] [<CommonParameters>]
```

### EveryHour
```
New-UDEndpointSchedule -Every <Int32> [-Repeat <Int32>] [-Consecutive] [-Hour] [<CommonParameters>]
```

### EveryDay
```
New-UDEndpointSchedule -Every <Int32> [-Repeat <Int32>] [-Consecutive] [-Day] [<CommonParameters>]
```

### Cron
```
New-UDEndpointSchedule [-Consecutive] [-Cron <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a schedule for New-UDEndpoint. 

## EXAMPLES

### Example 1
```powershell
$Schedule = New-UDEndpointSchedule 10 -Second
New-UDEndpoint -Schedule $Schedule -Endpoint {
    $Cache:Processes = Get-Process
}
```

Caches processes every 10 seconds. 

## PARAMETERS

### -Consecutive

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Cron
A CRON expression that defines the endpoint schedule. 

```yaml
Type: String
Parameter Sets: Cron
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Day
The Every parameter refers to days.

```yaml
Type: SwitchParameter
Parameter Sets: EveryDay
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Every
The unit of time between scheduled runs. 

```yaml
Type: Int32
Parameter Sets: EverySecond, EveryMinute, EveryHour, EveryDay
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Hour
The Every parameter refers to hours.

```yaml
Type: SwitchParameter
Parameter Sets: EveryHour
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Minute
The Every parameter refers to minutes. 

```yaml
Type: SwitchParameter
Parameter Sets: EveryMinute
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Repeat

```yaml
Type: Int32
Parameter Sets: EverySecond, EveryMinute, EveryHour, EveryDay
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Second
The Every parameter refers to Seconds. 

```yaml
Type: SwitchParameter
Parameter Sets: EverySecond
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
