---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-PSUJobPipelineOutput

## SYNOPSIS

Gets the pipeline output written by a job. 

## SYNTAX

### ById
```
Get-PSUJobPipelineOutput -JobId <Int64> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### ByRunId
```
Get-PSUJobPipelineOutput -RunId <Guid> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### ByObject
```
Get-PSUJobPipelineOutput -Job <Job> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
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
App token to access the PowerShell Universal server. 

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
The name or URL of the PowerShell Universal server.

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
Whether to use integrated transport

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
The job for which to receive the pipeline input for. 

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
The job ID for which to receive the pipeline input for. 

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

### -UseDefaultCredentials
Use default Windows Credentials when connecting to PowerShell Universal.

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

### -RunId
The run ID (GUID) for this job. Requires JobRunId experimental feature. 

```yaml
Type: Guid
Parameter Sets: ByRunId
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