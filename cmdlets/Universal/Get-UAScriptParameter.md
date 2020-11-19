---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-UAScriptParameter

## SYNOPSIS
Returns parameters for a script.

## SYNTAX

### ById
```
Get-UAScriptParameter -ScriptId <Int64> [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### ByObject
```
Get-UAScriptParameter -Script <Script> [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
Returns parameters for a script.

## EXAMPLES

### Example 1
```
PS C:\> Get-UAScriptParameter -ScriptId 12
```

Returns parameters for script 12.

### Example 2
```
PS C:\> $Script = Get-UAScript -Name 'Script1.ps1'
PS C:\> Get-UAScriptParameter -Script $Script
```

Returns parameters for script 'Script1.ps1'

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
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Script
The script to return parameters for.
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
The ID of the script to return parameters for.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### UniversalAutomation.Script
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
