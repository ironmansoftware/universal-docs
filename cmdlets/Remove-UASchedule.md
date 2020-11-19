---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Remove-UASchedule

## SYNOPSIS
Removes a schedule for a script.

## SYNTAX

```
Remove-UASchedule [-Schedule] <Schedule> [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
Removes a schedule for a script.

## EXAMPLES

### Example 1
```
PS C:\> $Schedule = Get-UASchedule -Id 12
PS C:\> Remove-UASchedule -Schedule $Schedule
```

Removes schedule 12.

## PARAMETERS

### -AppToken
An app token to access the UA API.

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

### -ComputerName
The HTTP address of the UA REST API server.

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

### -Schedule
The schedule to remove.
Use Get-UASchedule to retrieve a Schedule object.

```yaml
Type: Schedule
Parameter Sets: (All)
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### UniversalAutomation.Schedule
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
