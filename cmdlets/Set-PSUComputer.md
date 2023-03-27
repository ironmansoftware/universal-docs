---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Set-PSUComputer

## SYNOPSIS
Updates a computer. 

## SYNTAX

### Id
```
Set-PSUComputer [-Id] <Int64> [-Maintenance <Boolean>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

### Computer
```
Set-PSUComputer [-Computer] <Computer> [-Maintenance <Boolean>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
Updates a computer. 

## EXAMPLES

### Example 1
```powershell
PS C:\> Set-PSUComputer -ComputerName computer1 -Maintenance $true
```

Enables maintenance mode for a computer. 

## PARAMETERS

### -AppToken
The app token used to connect to the PowerShell Universal server. 

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

### -Computer
The computer name or URL of the PowerShell Universal server. 

```yaml
Type: Computer
Parameter Sets: Computer
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -ComputerName
The name of the computer to update.

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
The ID of the computer to update. 

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
Whether to use the integrated environemnt.

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

### -Maintenance
Whether to enable or disable maintenance mode for this computer.

```yaml
Type: Boolean
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseDefaultCredentials
Whether to use Windows Authentication for this call.

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

### PowerShellUniversal.Computer

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
