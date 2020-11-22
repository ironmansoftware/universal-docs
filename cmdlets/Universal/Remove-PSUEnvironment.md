---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Remove-PSUEnvironment

## SYNOPSIS
Removes an environment from PowerShell Universal.

## SYNTAX

```
Remove-PSUEnvironment [-Environment] <ExecutionEnvironment> [-ComputerName <String>] [-AppToken <String>]
 [<CommonParameters>]
```

## DESCRIPTION
{{ Fill in the Description }}

## EXAMPLES

### Example 1
```powershell
PS C:\> Remove-PSUEnvironment -Environment (Get-PSUEnvironment -Id 1)
```

Removes environment with ID 1 from the system.

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

### -Environment
The environment to remove. Use Get-PSUEnvironment to retrieve an environment.

```yaml
Type: ExecutionEnvironment
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

### UniversalAutomation.ExecutionEnvironment

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[New-PSUEnvironment](New-PSUEnvironment.md)
[Set-PSUEnvironment](Set-PSUEnvironment.md)
[Get-PSUEnvironment](Get-PSUEnvironment.md)