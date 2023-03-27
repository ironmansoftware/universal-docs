---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Start-PSUTerminalInstance

## SYNOPSIS
Starts a terminal instance. 

## SYNTAX

```
Start-PSUTerminalInstance -Terminal <Terminal> [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
Starts a terminal instance. Use Get-PSUTerminal to return terminal configurations. 

## EXAMPLES

### Example 1
```powershell
PS C:\> $Terminal = Get-PSUTerminal | Where-Object Name -eq 'Terminal1'
PS C:\> Start-PSUTerminalInstance -Terminal $Terminal
```

Starts a new instance of Terminal1

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
Not supported

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

### -Terminal
The terminal configuration to start. Use Get-PSUTerminal to return terminal configurations.

```yaml
Type: Terminal
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -UseDefaultCredentials
Whether to use Windows Authentication against the PowerShell Universal server.

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

### PowerShellUniversal.Terminal

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
