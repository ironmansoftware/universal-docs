---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-PSUTerminalInstance

## SYNOPSIS
Returns running terminal instances.

## SYNTAX

### All (Default)
```
Get-PSUTerminalInstance [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-Integrated]
 [<CommonParameters>]
```

### Id
```
Get-PSUTerminalInstance [-Id] <Int64> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
Returns running terminal instances. Terminal instances can be started from the admin console or by using Start-PSUTerminalInstance.

## EXAMPLES

### Example 1
```powershell
PS C:\> $Terminal = Get-PSUTerminal | Where-Object Name -eq 'Terminal1'
PS C:\> Start-PSUTerminalInstance -Terminal $Terminal 
PS C:\> Get-PSUTerminalInstance
```

Starts a new instance of Terminal1 and then returns all running terminal instances.

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

### -Id
The ID of the terminal instance to return.

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

### None

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
