---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDDynamic

## SYNOPSIS
Defines a new dynamic region in a dashboard.

## SYNTAX

```
New-UDDynamic [-Id <String>] [-ArgumentList <Object[]>] [-Content] <Endpoint> [-AutoRefresh]
 [-AutoRefreshInterval <Int32>] [-LoadingComponent <ScriptBlock>] [<CommonParameters>]
```

## DESCRIPTION
Defines a new dynamic region in a dashboard.
Dynamic regions are used for loading data when the page is loaded or for loading data dynamically through user interaction or auto-reloading.

## EXAMPLES

### EXAMPLE 1
```
A simple dynamic region that executes when the user loads the page.
```

New-UDDynamic -Content {
    New-UDTypography -Text (Get-Date)
}

### EXAMPLE 2
```
A dynamic region that refreshes every 3 seconds
```

New-UDDynamic -Content {
    New-UDTypography -Text (Get-Date)
} -AutoRefresh -AutoRefreshInterval 3

### EXAMPLE 3
```
A dynamic region that is updated when a button is clicked.
```

New-UDDynamic -Content {
    New-UDTypography -Text (Get-Date)
} -Id 'dynamic'

New-UDButton -Text 'Refresh' -OnClick {
    Sync-UDElement -Id 'dynamic'
}

## PARAMETERS

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

### -ArgumentList
Arguments to pass to this dynamic endpoint.

```yaml
Type: Object[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Content
The content of this dynamic region.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -AutoRefresh
Whether this dynamic region should refresh on an interval.

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

### -AutoRefreshInterval
The amount of seconds between refreshes for this dynamic region.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: 10
Accept pipeline input: False
Accept wildcard characters: False
```

### -LoadingComponent
A component to display while this dynamic region is loading.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: {}
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
