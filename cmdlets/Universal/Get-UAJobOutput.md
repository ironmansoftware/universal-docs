---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-UAJobOutput

## SYNOPSIS
Returns stream output for a job.

## SYNTAX

### ById
```
Get-UAJobOutput -JobId <Int64> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [<CommonParameters>]
```

### ByObject
```
Get-UAJobOutput -Job <Job> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [<CommonParameters>]
```

## DESCRIPTION
Returns stream output for a job.
This includes error, warning, information, debug and verbose.
Use Get-UAJobPipelineOutput to receive pipeline output.

## EXAMPLES

### Example 1
```
PS C:\> Get-UAJobOutput -JobId 10
```

Returns output for job 10.

### Example 2
```
PS C:\> $Job = Get-UAJob -Id 12
PS C:\> Get-UAJobOutput -Job $Job
```

Returns output for job 12.

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

### -Job
The job to return output for.

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
The ID of the job to return output for.

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
