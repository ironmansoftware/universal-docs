---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-UAScriptHistory

## SYNOPSIS
Returns the git history for a script.

## SYNTAX

### ById
```
Get-UAScriptHistory -ScriptId <Int64> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [<CommonParameters>]
```

### ByObject
```
Get-UAScriptHistory -Script <Script> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [<CommonParameters>]
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

### -Script
The script to return history for.
Use Get-UAScript to get a Script object.

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
The ID of the script to return history for.

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

### UniversalAutomation.Script
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
