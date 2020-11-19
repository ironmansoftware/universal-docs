---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUTrigger

## SYNOPSIS

Creates a new Automation trigger in PowerShell Universal. 

## SYNTAX

```
New-PSUTrigger -Name <String> -EventType <EventType> -TriggerScript <Script> [-Script <Script>]
 [-Dashboard <Dashboard>] [-Environment <String>] [-ComputerName <String>] [-AppToken <String>]
 [<CommonParameters>]
```

## DESCRIPTION

Creates a new Automation trigger in PowerShell Universal. Powershell Universal Automation triggers allow you to execute scripts based on events within PowerShell Universal. You can run scripts when other scripts fail, dashboards stop or when the server is starting up. 

Triggers are stored within the ./universal/triggers.ps1 file. 

You can also use this cmdlet to create triggers through the REST API.

## EXAMPLES

### Example 1
```powershell
New-PSUTrigger -Name 'Script Failed' -EventType JobFailed -TriggerScript 'ScriptFailed.ps1' 
```

Creates a new trigger that calls the ScriptFailed.ps1 file when any job within PowerShell Universal fails. 

### Example 2
```powershell
New-PSUTrigger -Name 'Dashboard Stopped' -Dashboard 'MyDashboard' -EventType DashboardStopped -TriggerScript 'DashboardStopped.ps1' 
```

Creates a new trigger that calls the DashboardStopped.ps1 file when the dashboard MyDashboard stops. 

### Example 3
```powershell
New-PSUTrigger -Name 'Server Started' -EventType ServerStarted -TriggerScript 'LogServerStart.ps1' 
```

Creates a new trigger that calls the LogServerStart.ps1 file when the PowerShell Universal server is started. 

## PARAMETERS

### -AppToken
 The app token for accessing the PowerShell Universal Management API.

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
The computer name or URL of the Powershell Universal server. 

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

### -Dashboard

Triggers for a specific dashboard.

```yaml
Type: Dashboard
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Environment

The environment to run the triggered script in.

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

The event that causes this trigger.

```yaml
Type: EventType
Parameter Sets: (All)
Aliases:
Accepted values: JobCanceled, JobFailed, JobCompleted, JobStarted, JobFeedbackRequested, ServerStarted, ServerStopped, DashboardStarted, DashboardStopped

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name

The name of this trigger. This needs to be unique. 

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

### -Script

The script that causes this trigger.

```yaml
Type: Script
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -TriggerScript

The script to trigger when this trigger is triggered.

```yaml
Type: Script
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

[New-PSUScript](New-PSUScript.md)
[New-PSUDashboard](New-PSUDashboard.md)
[Get-PSUDashboard](Get-PSUDashboard.md)
[Get-PSUScript](Get-PSUScript.md)