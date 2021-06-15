---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Set-PSUTrigger

## SYNOPSIS
Updates an existing PowerShell Universal Automation trigger.

## SYNTAX

### Id
```
Set-PSUTrigger [-Id] <Int64> [-Name <String>] [-EventType <EventType>] [-Script <String>]
 [-TriggerScript <String>] [-Environment <String>] [-Dashboard <String>] [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

### Trigger
```
Set-PSUTrigger [-Trigger] <Trigger> [-Name <String>] [-EventType <EventType>] [-Script <String>]
 [-TriggerScript <String>] [-Environment <String>] [-Dashboard <String>] [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

## DESCRIPTION
{{ Fill in the Description }}

## EXAMPLES

### Example 1
```powershell
PS C:\> {{ Add example code here }}
```

{{ Add example description here }}

## PARAMETERS

### -AppToken
{{ Fill AppToken Description }}

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
{{ Fill ComputerName Description }}

```yaml
Type: String
Parameter Sets: (All)
Aliases: Uri

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Dashboard
{{ Fill Dashboard Description }}

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

### -Environment
{{ Fill Environment Description }}

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

### -EventType
{{ Fill EventType Description }}

```yaml
Type: EventType
Parameter Sets: (All)
Aliases:
Accepted values: JobCanceled, JobFailed, JobCompleted, JobStarted, JobFeedbackRequested, ServerStarted, ServerStopped, DashboardStarted, DashboardStopped

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id
{{ Fill Id Description }}

```yaml
Type: Int64
Parameter Sets: Id
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
{{ Fill Name Description }}

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

### -Script
{{ Fill Script Description }}

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

### -Trigger
{{ Fill Trigger Description }}

```yaml
Type: Trigger
Parameter Sets: Trigger
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -TriggerScript
{{ Fill TriggerScript Description }}

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

### -UseDefaultCredentials
Use default credentials when connecting to the management API

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### UniversalAutomation.Trigger

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
