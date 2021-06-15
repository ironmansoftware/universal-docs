---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-UDDashboardFramework

## SYNOPSIS

Returns Universal Dashboard frameworks currently installed on the system. 

## SYNTAX

```
Get-UDDashboardFramework [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [<CommonParameters>]
```

## DESCRIPTION
Returns Universal Dashboard frameworks currently installed on the system. Universal Dashboard frameworks are versions of the JavaScript and PowerShell modules used to define dashboards. 

You can install multiple versions of a framework in Universal Dashboard. 

## EXAMPLES

### Example 1
```
PS C:\> Get-UDDashboardFramework -ComputerName 'http://localhost:5000' -AppToken 'appToken'
```

Returns all dashboard frameworks currently installed on the server. 

## PARAMETERS

### -AppToken

The app token used to call the PowerShell Universal Management API.

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

The computer name or URL to the PowerShell Universal server. 

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

### None
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
