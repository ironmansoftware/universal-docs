---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-UDPage

## SYNOPSIS
Creates a page within a dashboard. 

## SYNTAX

### Simple (Default)
```
New-UDPage [-Id <String>] -Name <String> [-Url <String>] [-Description <String>] [-Role <String[]>]
 -Content <Endpoint> [-DefaultHomePage] [[-Title] <String>] [-OnLoading <ScriptBlock>]
 [-NavigationLayout <String>] [-Navigation <Hashtable[]>] [-Logo <String>] [-HeaderPosition <String>]
 [-HeaderColor <DashboardColor>] [-HeaderBackgroundColor <DashboardColor>] [-HeaderContent <Endpoint>]
 [-HideUserName] [-HideNavigation] [-Icon <Object>] [-LoadTitle <Endpoint>] [-Static] [<CommonParameters>]
```

### Advanced
```
New-UDPage [-Id <String>] -Name <String> [-Url <String>] [-Description <String>] [-Role <String[]>]
 -Content <Endpoint> [-DefaultHomePage] [[-Title] <String>] [-Blank] [-OnLoading <ScriptBlock>]
 [-HeaderPosition <String>] [-HeaderColor <DashboardColor>] [-HeaderBackgroundColor <DashboardColor>]
 [-HideUserName] [-HideNavigation] [-Icon <Object>] [-Static] [<CommonParameters>]
```

### DynamicNav
```
New-UDPage [-Id <String>] -Name <String> [-Url <String>] [-Description <String>] [-Role <String[]>]
 -Content <Endpoint> [-DefaultHomePage] [[-Title] <String>] [-OnLoading <ScriptBlock>]
 [-NavigationLayout <String>] [-Logo <String>] [-LoadNavigation <Endpoint>] [-HeaderPosition <String>]
 [-HeaderColor <DashboardColor>] [-HeaderBackgroundColor <DashboardColor>] [-HeaderContent <Endpoint>]
 [-HideUserName] [-HideNavigation] [-Icon <Object>] [-LoadTitle <Endpoint>] [-Static] [<CommonParameters>]
```

## DESCRIPTION
Creates a page within a dashboard. 

## EXAMPLES

## PARAMETERS

### -Blank
Creates a page without a header. 

```yaml
Type: SwitchParameter
Parameter Sets: Advanced
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Content
The content of this page. 

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DefaultHomePage
Whether this page is the default home page. Only one page can be a default home page. 

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Description
The description of this page. 

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

### -HeaderBackgroundColor
The header background color. 

```yaml
Type: DashboardColor
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -HeaderColor
The header foreground color. 

```yaml
Type: DashboardColor
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -HeaderContent
Additional header content to include. 

```yaml
Type: Endpoint
Parameter Sets: Simple, DynamicNav
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -HeaderPosition
How to position the header. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:
Accepted values: absolute, fixed, relative, static, sticky

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -HideNavigation
Whether to hide the navigation. 

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

### -HideUserName
Whether to hide the user name when using an authenticated dashboard. 

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

### -Icon
The icon to display in the navigation for this page. 

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id
The ID of this page. 

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

### -LoadNavigation
Custom navigation to load dynamically. 

```yaml
Type: Endpoint
Parameter Sets: DynamicNav
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -LoadTitle
Loads the title of this page dynamically. 

```yaml
Type: Endpoint
Parameter Sets: Simple, DynamicNav
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Logo
The URL of the logo to display in the header. 

```yaml
Type: String
Parameter Sets: Simple, DynamicNav
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
The name of this page.

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

### -Navigation
The static navigation to display on this page.

```yaml
Type: Hashtable[]
Parameter Sets: Simple
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NavigationLayout
How to display the navigation.

```yaml
Type: String
Parameter Sets: Simple, DynamicNav
Aliases:
Accepted values: Temporary, Permanent

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnLoading
Content to display when the page is loading. 

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Role
The role required to view this page.

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

### -Title
The title to display in the header and title bar of this page.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Url
The URL of this page. 

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

### -Static
A static page's content is not load dynamically when a user visits it and instead is constructed when the dashboard is started.

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
