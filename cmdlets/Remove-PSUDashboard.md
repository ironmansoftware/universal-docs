---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Remove-PSUDashboard

## SYNOPSIS
Removes a dashboard from PowerShell Universal.

## SYNTAX

### All (Default)
```
Remove-PSUDashboard [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-Integrated]
 [<CommonParameters>]
```

### Dashboard
```
Remove-PSUDashboard [-Dashboard] <Dashboard> [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

### Id
```
Remove-PSUDashboard [-Id] <Int64> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
Removes a dashboard from PowerShell Universal.

## EXAMPLES

### Example 1
```powershell
PS C:\> Get-PSUDashboard -Name Dashboard | Remove-PSUDashboard
```

## PARAMETERS

### -AppToken
An app token used to connect to PSU. 

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
The URL of the PSU server. 

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
The Id of the dashboard to remove.

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

### -Dashboard
The dashboard to remove. Use Get-PSUDashboard to retrieve one or more dashboards.

```yaml
Type: Dashboard
Parameter Sets: Dashboard
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Integrated
No supported. 

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
Whether to use default Windows credentials when connecting to PSU. 

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

### PowerShellUniversal.Dashboard

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
