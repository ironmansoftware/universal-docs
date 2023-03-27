---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-PSUScriptHistory

## SYNOPSIS
Returns the git history for a script.

## SYNTAX

### ById
```
Get-PSUScriptHistory -ScriptId <Int64> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### ByObject
```
Get-PSUScriptHistory -Script <Script> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
Returns the git history for a script.

## EXAMPLES

### Example 1
```
PS C:\> Get-UAScriptHistory -ScriptId 12
```

Returns the script history for script with ID 12.

### Example 2
```
PS C:\> $Script = Get-UAScript -Name 'Script1.ps1'
PS C:\> Get-UAScriptHistory -Script $Script
```

Returns the history for script 'Script1.ps1'

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

### -Script
The script for which to receive history.

```yaml
Type: Script
Parameter Sets: ByObject
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -ScriptId
The script ID for which to receive history.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### UniversalAutomation.Script
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
