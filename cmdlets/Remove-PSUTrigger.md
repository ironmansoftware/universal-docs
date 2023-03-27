---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Remove-PSUTrigger

## SYNOPSIS
{{ Fill in the Synopsis }}

## SYNTAX

### All (Default)
```
Remove-PSUTrigger [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-Integrated]
 [<CommonParameters>]
```

### Trigger
```
Remove-PSUTrigger [-Trigger] <Trigger> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### Id
```
Remove-PSUTrigger [-Id] <Int64> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
{{ Fill in the Description }}

## EXAMPLES

### Example 1
```powershell
PS C:\> {{ Add example code here }}
```

{{ Add example description here }}

## PARAMETERS

### -AppToken
{{ Fill AppToken Description }}

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
{{ Fill ComputerName Description }}

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
The Id of the trigger to remove.

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

### -Trigger
{{ Fill Trigger Description }}

```yaml
Type: Trigger
Parameter Sets: Trigger
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
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

### -Integrated
Executes the command internally rather than using the Management API. Only works when running script from within PowerShell Universal. 

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

### UniversalAutomation.Trigger

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
