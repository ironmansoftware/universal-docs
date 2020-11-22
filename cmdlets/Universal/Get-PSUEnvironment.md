---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-PSUEnvironment

## SYNOPSIS
Returns the environments defined in PowerShell Universal.

## SYNTAX

### All (Default)
```
Get-PSUEnvironment [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### Id
```
Get-PSUEnvironment [-Id] <Int64> [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
Returns the environments defined in PowerShell Universal.

## EXAMPLES

### Example 1
```powershell
PS C:\> Get-PSUEnvironment
```

Returns all the environments.

### Example 2
```powershell
PS C:\> Get-PSUEnvironment -Id 1
```

Returns the environment with ID 1. 

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

### -Id
The ID of the environment.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[New-PSUEnvironment](New-PSUEnvironment.md)
[Remove-PSUEnvironment](Remove-PSUEnvironment.md)
[Set-PSUEnvironment](Set-PSUEnvironment.md)