---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Wait-UAJob

## SYNOPSIS
Waits for a job to finish.

## SYNTAX

### ById
```
Wait-UAJob -JobId <Int64> [-Timeout <Int32>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [<CommonParameters>]
```

### ByObject
```
Wait-UAJob -Job <Job> [-Timeout <Int32>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [<CommonParameters>]
```

## DESCRIPTION
Waits for a job to finish.

## EXAMPLES

### Example 1
```
PS C:\> $Job = Get-UAJob -Id 12
PS C:\> Wait-UAJob -Job $Job
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

### -Job
The job to wait for.
Use Get-UAJob to retrieve a Job object.

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
