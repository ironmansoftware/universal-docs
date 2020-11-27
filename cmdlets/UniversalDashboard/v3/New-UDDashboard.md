---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDDashboard

## SYNOPSIS
Creates a new dashboard.

## SYNTAX

### Content
```
New-UDDashboard [-Title <String>] -Content <Endpoint> [-Theme <Hashtable>] [-Scripts <String[]>]
 [-Stylesheets <String[]>] [-Logo <String>] [-DefaultTheme <String>] [<CommonParameters>]
```

### Pages
```
New-UDDashboard [-Title <String>] -Pages <Hashtable[]> [-Theme <Hashtable>] [-Scripts <String[]>]
 [-Stylesheets <String[]>] [-Logo <String>] [-DefaultTheme <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new dashboard.
This component is the root element for all dashboards.
You can define content, pages, themes and more.

## EXAMPLES

### EXAMPLE 1
```
Creates a new dashboard with a single page.
```

New-UDDashboard -Title 'My Dashboard' -Content {
    New-UDTypography -Text 'Hello, world!'
}

### EXAMPLE 2
```
Creates a new dashboard with multiple pages.
```

$Pages = @(
    New-UDPage -Name 'HomePage' -Content {
        New-UDTypography -Text 'Home Page'
    }
    New-UDPage -Name 'Page2' -Content {
        New-UDTypography -Text 'Page2'
    }
)

New-UDDashboard -Title 'My Dashboard' -Pages $Pages

## PARAMETERS

### -Title
The title of the dashboard.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: PowerShell Universal Dashboard
Accept pipeline input: False
Accept wildcard characters: False
```

### -Content
The content for this dashboard.
When using content, it creates a dashboard with a single page.

```yaml
Type: Endpoint
Parameter Sets: Content
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Pages
Pages for this dashboard.
Use New-UDPage to define a page and pass an array of pages to this parameter.

```yaml
Type: Hashtable[]
Parameter Sets: Pages
Aliases:

Required: True
Position: Named
Default value: @()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Theme
The theme for this dashboard.
You can define a theme with New-UDTheme.

```yaml
Type: Hashtable
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: @{}
Accept pipeline input: False
Accept wildcard characters: False
```

### -Scripts
JavaScript files to run when this dashboard is loaded.
These JavaScript files can be absolute and hosted in a third-party CDN or you can host them yourself with New-PSUPublishedFolder.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: @()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Stylesheets
CSS files to run when this dashboard is loaded.
These CSS files can be absolute and hosted in a third-party CDN or you can host them yourself with New-PSUPublishedFolder.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: @()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Logo
A logo to display in the navigation bar.
You can use New-PSUPublishedFolder to host this logo file.

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

### -DefaultTheme
The default theme to show when the page is loaded.
The default is to use the light theme.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: Light
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
