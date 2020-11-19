---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-UAJobPipelineOutput (Get-PSUJobPipelineOutput)

## SYNOPSIS

Gets the pipeline output written by a job. 

## SYNTAX

### ById
```
Get-UAJobPipelineOutput -JobId <Int64> [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### ByObject
```
Get-UAJobPipelineOutput -Job <Job> [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
Gets the pipeline output written by a job. Pipeline output that is written to a job is stored as CLIXML and can be retrieved by this cmdlet. 

## EXAMPLES

### Example 1
```
PS C:\> Get-UAJobPipelineOutput -JobId 10
```

Returns pipeline output for job 10.

### Example 2
```
PS C:\> $Job = Get-UAJob -Id 12
PS C:\> Get-UAJobPipelineOutput -Job $Job
```

Returns pipeline output for job 12.

## PARAMETERS

### -AppToken
The AppToken that is used for calling the PowerShell Universal Management API. You can also call Connect-PSUServer before calling this cmdlet to set the AppToken for the entire session.

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
Specifies the computer name or URL that should be called when accessing the PowerShell Universal Management API. You can also use Connect-PSUServer before calling this cmdlet to set the computer name for the entire session. 

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

### -Job
The job to retrieve pipeline output for. You can retrieve jobs with Get-PSUJob.

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
The ID of the job to retrieve pipeline output for. 

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### UniversalAutomation.Job
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[Get-PSUJob](Get-UAJob.md)