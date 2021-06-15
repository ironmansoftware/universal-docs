---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUDashboard

## SYNOPSIS
Creates a new dashboard.

## SYNTAX

### FilePath
```
New-PSUDashboard -FilePath <String> [-BaseUrl <String>] -Name <String> [-Framework <DashboardFramework>]
 [-Environment <String>] [-GrantAppToken] [-Authenticated] [-Role <String[]>] [-DisableAutoStart]
 [-Component <DashboardComponent[]>] [-SessionTimeout <Int32>] [-AutoDeploy] [-Description <String>]
 [-Credential <String>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [<CommonParameters>]
```

### Content
```
New-PSUDashboard -Content <ScriptBlock> [-BaseUrl <String>] -Name <String> [-Framework <DashboardFramework>]
 [-Environment <String>] [-GrantAppToken] [-Authenticated] [-Role <String[]>] [-DisableAutoStart]
 [-Component <DashboardComponent[]>] [-SessionTimeout <Int32>] [-AutoDeploy] [-Description <String>]
 [-Credential <String>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [<CommonParameters>]
```

## DESCRIPTION
Creates a new dashboard. Dashboards allow you to create websites with PowerShell. 

## EXAMPLES

### Example 1
```powershell
New-PSUDashboard -Name 'Dashboard' -BaseUrl '/dashboard' -FilePath "dashboard.ps1"
```

Creates a dashboard using the dashboard.ps1 file in the repository directory and serves it at the base URL of /dashboard. 

## PARAMETERS

### -AppToken
An app token used to connect to the management console.

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
Whether authentication is required for this dashboard.

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

### -AutoDeploy
Whether to automatically deploy the dashboard when it changes.

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

### -BaseUrl
The base URL to serve the dashboard on.

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

### -Component
A list of component modules to import.

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

### -ComputerName
The URI of the management API.

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

### -Content
A script block containing dashboard content.

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

### -Credential
The user credential variable to use when starting the dashboard.

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

### -Description
A description of the dashboard.

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

### -DisableAutoStart
Whether to disable starting the dashboard when PSU starts.

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
The environment to use with the dashboard.

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
The file path of the dashboard PowerShell script that defines this dashboard.

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
The Universal Dashboard framework to use for this dashboard.

```yaml
Type: DashboardFramework
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -GrantAppToken
Whether to automatically grant an app token to users accessing the dashboard. This is used if your dashboard requires access to the management API.

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

### -Role
An array of roles that can access the dashboard.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SessionTimeout
The number of minutes before a session will time out in the dashboard.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

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
