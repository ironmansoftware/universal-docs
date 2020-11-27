---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDPage

## SYNOPSIS
Defines a new page.

## SYNTAX

### Simple (Default)
```
New-UDPage [-Name] <String> [-Content] <Endpoint> [[-Url] <String>] [-DefaultHomePage] [[-Title] <String>]
 [-Id <String>] [-OnLoading <ScriptBlock>] [-Role <String>] [-NavigationLayout <String>]
 [-Navigation <Hashtable[]>] [-Logo <String>] [<CommonParameters>]
```

### Advanced
```
New-UDPage [-Name] <String> [-Content] <Endpoint> [[-Url] <String>] [-DefaultHomePage] [[-Title] <String>]
 [-Blank] [-Id <String>] [-OnLoading <ScriptBlock>] [-Role <String>] [<CommonParameters>]
```

### DynamicNav
```
New-UDPage [-Name] <String> [-Content] <Endpoint> [[-Url] <String>] [-DefaultHomePage] [[-Title] <String>]
 [-Id <String>] [-OnLoading <ScriptBlock>] [-Role <String>] [-NavigationLayout <String>] [-Logo <String>]
 [-LoadNavigation <Endpoint>] [<CommonParameters>]
```

## DESCRIPTION
Defines a new page.
Dashboards can contain multiple pages that each contain different components.

## EXAMPLES

### EXAMPLE 1
```
Creates a basic page.
```

New-UDPage -Name 'Test' -Content {
    New-UDTypography -Text 'Page'
}

## PARAMETERS

### -Name
The name of the page.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Content
The content of the page.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases: Endpoint

Required: True
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Url
The URL for the page.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DefaultHomePage
Whether this page is the default home page.
Only one page can be the default home page.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Title
The title of the page.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 5
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Blank
Whether to define a blank page.
Blank pages won't have a navigation bar.

```yaml
Type: SwitchParameter
Parameter Sets: Advanced
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id
The ID of this component.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: [Guid]::NewGuid()
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnLoading
A component to return while this page is loading.

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
The role of the user that is allowed to access this page.

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

### -NavigationLayout
How the navigation is layed out on the page.

```yaml
Type: String
Parameter Sets: Simple, DynamicNav
Aliases:

Required: False
Position: Named
Default value: Temporary
Accept pipeline input: False
Accept wildcard characters: False
```

### -Navigation
Custom navigation to show for this page.
You can use New-UDList and New-UDListItem to define custom navigation links.

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

### -Logo
The logo to display on this page.

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

### -LoadNavigation
An endpoint that is called when loading the navigation for the page.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
