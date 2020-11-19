---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-UASchedule

## SYNOPSIS
Creates a new schedule within UA.

## SYNTAX

### Cron
```
New-UASchedule [-Script] <Script> [-Cron] <String> [-Credential <Variable>] [-TimeZone <String>]
 [-Environment <String>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### Continuous
```
New-UASchedule [-Script] <Script> [-Credential <Variable>] [-TimeZone <String>] [-Continuous]
 [-Delay <TimeSpan>] [-DelaySecond <Int32>] [-DelayMinute <Int32>] [-DelayHour <Int32>] [-Environment <String>]
 [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### OneTime
```
New-UASchedule [-Script] <Script> [-Credential <Variable>] [-TimeZone <String>] [-Environment <String>]
 [-OneTime <DateTime>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new schedule within UA.
Schedules allow you to automate when jobs run and run jobs continously.

## EXAMPLES

### Example 1
```
PS C:\> $Script = Get-UAScript -Name 'Script1.ps1'
PS C:\> New-UASchedule -Script $Script -Cron '*/5 * * * *'
```

Creates a new schedule that runs every five minutes.

### Example 2
```
PS C:\> $Password = Get-UAVariable -Name 'password'
PS C:\> $Credential = New-UACredential -Name 'adam' -Password $Password
PS C:\> $Script = Get-UAScript -Name 'Script1.ps1'
PS C:\> New-UASchedule -Script $Script -Cron '*/5 * * * *'
```

Creates a new schedule that runs every five minutes as 'adam'.

### Example 3
```
PS C:\> $Script = Get-UAScript -Name 'Script1.ps1'
PS C:\> New-UASchedule -Script $Script -Continous -DelayMinute 5
```

Creates a schedule that runs conintously.
It will start a new job once the previous one finishes with a delay of 5 minutes inbetween executions.

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

### -Continuous
Runs a job continously with an optional delay between executions.

```yaml
Type: SwitchParameter
Parameter Sets: Continuous
Aliases:

Required: True
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
A credential for the user to run the job as.
Use New-UACredential to create this credential object.

```yaml
Type: Variable
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Cron
The CRON schedule to use for this schedule.

```yaml
Type: String
Parameter Sets: Cron
Aliases:

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Delay
The delay inbetween continous job executions.

```yaml
Type: TimeSpan
Parameter Sets: Continuous
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DelayHour
The delay in hours inbetween continous job executions.

```yaml
Type: Int32
Parameter Sets: Continuous
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DelayMinute
The delay in minutes inbetween continous job executions.

```yaml
Type: Int32
Parameter Sets: Continuous
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DelaySecond
The delay in seconds inbetween continous job executions.

```yaml
Type: Int32
Parameter Sets: Continuous
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Script
The script to schedule.
Use Get-UAScript to retrieve a script object.

```yaml
Type: Script
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -TimeZone
The TimeZone to execute the script in.
By default, it runs in the current user's time zone.

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

### -OneTime
{{ Fill OneTime Description }}

```yaml
Type: DateTime
Parameter Sets: OneTime
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

### UniversalAutomation.Script
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
