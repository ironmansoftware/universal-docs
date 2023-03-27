---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Invoke-PSUTerminalCommand

## SYNOPSIS
Invokes a command in a terminal instance.

## SYNTAX

```
Invoke-PSUTerminalCommand -TerminalInstance <TerminalInstance> -Command <String> [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
Invokes a command in a terminal instance. You can start new terminal instances with Start-PSUTerminalInstance and return running instances with Get-PSUTerminalInstance.

## EXAMPLES

### Example 1
```powershell
PS C:\> $Terminal = Get-PSUTerminal | Where-Object Name -eq 'Terminal1'
PS C:\> Start-PSUTerminalInstance -Terminal $Terminal 
PS C:\> $Instance = Get-PSUTerminalInstance
PS C:\> Invoke-PSUTerminalCommand -TerminalInstance $Instance -Command 'Write-Host "Hello, World!"'
```

Creates a new terminal instance of Terminal1 and then invokes a command within it. 

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

### -Command
The command to invoke

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
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
The terminal instance within which to invoke the command. Use Get-PSUTerminalInstance to return running instances. 

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
The terminal configuration to start. Use Get-PSUTerminal to return terminal configurations.

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
