---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Stop-PSUTerminalInstance

## SYNOPSIS
Stops a running terminal instance. 

## SYNTAX

```
Stop-PSUTerminalInstance -TerminalInstance <TerminalInstance> [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
Stops a running terminal instance. You can retrieve terminal instances by using Get-PSUTerminalInstance. 

## EXAMPLES

### Example 1
```powershell
PS C:\> $Terminal = Get-PSUTerminal | Where-Object Name -eq 'Terminal1'
PS C:\> Start-PSUTerminalInstance -Terminal $Terminal 
PS C:\> Get-PSUTerminalInstance | Stop-PSUTerminalInstance
```

Starts a new terminal instance and then stops it. 

## PARAMETERS

### -AppToken
An App Token for authenticating against the PowerShell Universal server. 

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
Not Supported

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

### -TerminalInstance
The terminal instance to stop. Use Get-PSUTerminalInstance to return running instances.

```yaml
Type: TerminalInstance
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -UseDefaultCredentials
Use Windows Authentication.

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

### PowerShellUniversal.TerminalInstance

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
