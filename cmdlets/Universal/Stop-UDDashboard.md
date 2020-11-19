---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Stop-UDDashboard (Stop-PSUDashboard)

## SYNOPSIS
Stops a PowerShell Universal dashboard.

## SYNTAX

```
Stop-UDDashboard -Dashboard <Dashboard> [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
Stops a PowerShell Universal dashboard. Use Get-PSUDashboard to retrieve dashboards to stop. 

## EXAMPLES

### Example 1
```
PS C:\> Get-PSUDashboard | Stop-PSUDashboard
```

Stops all dashboards on the server.

## PARAMETERS

### -AppToken
The AppToken that is used for calling the PowerShell Universal Management API. You can also call Connect-PSUServer before calling this cmdlet to set the AppToken for the entire session.

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
Specifies the computer name or URL that should be called when accessing the PowerShell Universal Management API. You can also use Connect-PSUServer before calling this cmdlet to set the computer name for the entire session. 

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

### -Dashboard
The dashboard to stop. 

```yaml
Type: Dashboard
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### UniversalAutomation.Dashboard
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[Get-PSUDashboard](Get-PSUDashboard.md)
[Start-PSUDashboard](Start-UDDashboard.md)