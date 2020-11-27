---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDDrawer

## SYNOPSIS
Creates a new drawer.

## SYNTAX

```
New-UDDrawer [[-Id] <String>] [[-Children] <ScriptBlock>] [[-Variant] <String>] [[-Anchor] <String>]
 [<CommonParameters>]
```

## DESCRIPTION
Creates a new drawer.
A drawer is a navigational component that is typically used for navigating between pages.
It can be used with New-UDAppBar to provide a custom nav bar.

## EXAMPLES

### EXAMPLE 1
```
Creates a custom navbar using New-UDDrawer
```

$Drawer = New-UDDrawer -Id 'drawer' -Children {
    New-UDList -Content {
        New-UDListItem -Id 'lstHome' -Label 'Home' -OnClick { 
            Set-TestData 'Home'
            } -Content {
                New-UDListItem -Id 'lstNested' -Label 'Nested' -OnClick {
                Set-TestData 'Nested'
                }
            } 
    }
}

New-UDElement -Tag 'main' -Content {
    New-UDAppBar -Children { New-UDTypography -Text 'Hello' -Paragraph } -Position relative -Drawer $Drawer
}

## PARAMETERS

### -Id
The ID of the component.
It defaults to a random GUID.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: [Guid]::NewGuid()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Children
Navgiation controls to show within the drawer.
Use New-UDList and New-UDListItem to generate links within the drawer.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases: Content

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Variant
{{ Fill Variant Description }}

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: Temporary
Accept pipeline input: False
Accept wildcard characters: False
```

### -Anchor
{{ Fill Anchor Description }}

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: Left
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
