---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Wait-PSUJob

## SYNOPSIS
Waits for a job to finish.

## SYNTAX

### ById
```
Wait-PSUJob -JobId <Int64> [-Timeout <Int32>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

### ByObject
```
Wait-PSUJob -Job <Job> [-Timeout <Int32>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
Waits for a job to finish.

## EXAMPLES

### Example 1
```
PS C:\> $Job = Get-PSUJob -Id 12
PS C:\> Wait-PSUJob -Job $Job
```

Waits for job 12 to finish.

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
Aliases: Uri

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Integrated
Executes the command internally rather than using the Management API. Only works when running script from within PowerShell Universal. 

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

### -Job
The job to wait for.
Use Get-PSUJob to retrieve a Job object.

```yaml
Type: Job
Parameter Sets: ByObject
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -JobId
The ID of the job to wait for.

```yaml
Type: Int64
Parameter Sets: ById
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Timeout
The number of seconds to wait for the job to finish.

```yaml
Type: Int32
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

### UniversalAutomation.Job
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
