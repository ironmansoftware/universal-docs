---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version:
schema: 2.0.0
---

# Add-UDDashboard (New-PSUDashboard)

## SYNOPSIS

Creates a new dashboard within PowerShell Universal.

## SYNTAX

### FilePath
```
Add-UDDashboard -FilePath <String> -BaseUrl <String> -Name <String> -Framework <DashboardFramework>
 [-Environment <String>] [-GrantAppToken] [-Authenticated] [-Role <String>] [-DisableAutoStart]
 [-Component <DashboardComponent[]>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### Content
```
Add-UDDashboard -Content <ScriptBlock> -BaseUrl <String> -Name <String> -Framework <DashboardFramework>
 [-Environment <String>] [-GrantAppToken] [-Authenticated] [-Role <String>] [-DisableAutoStart]
 [-Component <DashboardComponent[]>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION

Creates a new dashboard within PowerShell Universal. Dashboards are websites developed with PowerShell. You can use this cmdlet to define dashboards based on path or content, select the dashboard framework and assign authentication and authorization. 

Dashboard configurations are stored in .universal/dashboards.ps1

You can also use this cmdlet to create dashboard through the REST API.

## EXAMPLES

### Example 1
```
New-PSUDashboard -Name 'Dashboard' -FilePath 'dashboard.ps1' -Framework "UniversalDashboard:Latest" -BaseUrl /dashboard
```

Creates a new dashboard named Dashboard that uses the latest dashboard framework. The dashboard file dashboard.ps1 is loaded when the dashboard is started. The dashboard's base URL is set to '/dashboard' which is the URL that must be visited to view the dashboard. 

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

### -Authenticated

Enables authentication for the dashboard. Dashboard authentication requires a license. 

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -BaseUrl

The URL that must be visited to view the dashboard. 

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

### -FilePath

The file path of the dashboard file. This file path can either be an absolute file path or a relative file path to the repository directory. 

```yaml
Type: String
Parameter Sets: FilePath
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Framework

The dashboard framework to use. When calling the REST API, you can use the cmdlet Get-PSUDashboardFramework to return available frameworks. You can also specify a string with the name of the framework, a colon and then the version of the framework (e.g. 'UniversalDashboard:3.2.0'). Use 'Latest' to specify the latest dashboard framework version (e.g. 'UniversalDashboard:Latest'). 

```yaml
Type: DashboardFramework
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -GrantAppToken
Specifies that an app token should be granted to users that access this dashboard. If the user already has an active app token, that one will be used instead. If they do not, a read-only app token will be issued to the user. The app token is available in the dashboard using the $PSUAppToken variable within the dashboard. 

This setting only works for authenticated dashboards. 

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
The name of the dashboard.

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

### -Component
Component libraries to load into the dashboard automatically. You can find which component libraries are available on the server by using Get-PSUDashboardComponent. 

```yaml
Type: DashboardComponent[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Content
The content of the dashboard. The cmdlets used within this content block will be based on the framework you select. 

```yaml
Type: ScriptBlock
Parameter Sets: Content
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DisableAutoStart
Prevents this dashboard from auto-starting when the server starts up or there are changes made to the dashboard's contents. You will have to manually start or restart the dashboard. 

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

### -Environment
The environment to use for this dashboard. You can use Get-PSUEnvironment to list the available environments. 

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

### -Role
The role required to access this dashboard. Dashboard authentication must be enabled for this to work. 

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[Get-PSUDashboard](Get-PSUDashboard.md)
[Start-UDDashboard](Start-UDDashboard.md)
[Stop-UDDashboard](Stop-UDDashboard.md)
[Get-PSUEnvironment](Get-PSUEnvironment.md)
[Get-UDDashboardFramework](Get-UDDashboardFramework.md)