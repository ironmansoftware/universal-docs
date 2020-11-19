---
external help file: UniversalDashboard.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-UDEndpointSchedule

## SYNOPSIS
{{ Fill in the Synopsis }}

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
{{ Fill in the Description }}

## EXAMPLES

### Example 1
```
PS C:\> {{ Add example code here }}
```

{{ Add example description here }}

## PARAMETERS

### -Consecutive
{{ Fill Consecutive Description }}

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

### -Cron
{{ Fill Cron Description }}

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
{{ Fill Day Description }}

```yaml
Type: SwitchParameter
Parameter Sets: EveryDay
Aliases:

Required: True
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Every
{{ Fill Every Description }}

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
{{ Fill Hour Description }}

```yaml
Type: SwitchParameter
Parameter Sets: EveryHour
Aliases:

Required: True
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Minute
{{ Fill Minute Description }}

```yaml
Type: SwitchParameter
Parameter Sets: EveryMinute
Aliases:

Required: True
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Repeat
{{ Fill Repeat Description }}

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
{{ Fill Second Description }}

```yaml
Type: SwitchParameter
Parameter Sets: EverySecond
Aliases:

Required: True
Position: Named
Default value: False
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
