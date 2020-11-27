---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDTabs

## SYNOPSIS
Creates a new set of tabs.

## SYNTAX

```
New-UDTabs [-Tabs] <ScriptBlock> [[-Id] <String>] [-RenderOnActive] [[-Orientation] <String>]
 [<CommonParameters>]
```

## DESCRIPTION
Creates a new set of tabs.
Tabs can be used to show lots of content on a single page.

## EXAMPLES

### EXAMPLE 1
```
Creates a basic set of tabs.
```

New-UDTabs -Tabs {
    New-UDTab -Text "Tab1" -Id 'Tab1' -Content {
        New-UDElement -Tag div -Id 'tab1Content' -Content { "Tab1Content"}
    }
    New-UDTab -Text "Tab2" -Id 'Tab2' -Content {
        New-UDElement -Tag div -Id 'tab2Content' -Content { "Tab2Content"}
    }
    New-UDTab -Text "Tab3" -Id 'Tab3' -Content {
        New-UDElement -Tag div -Id 'tab3Content' -Content { "Tab3Content"}
    }
}

### EXAMPLE 2
```
Creates a set of tabs that only render when they are clicked.
```

New-UDTabs -RenderOnActive -Id 'DynamicTabs' -Tabs {
    New-UDTab -Text "Tab1" -Id 'DynamicTab1' -Dynamic -Content {
        New-UDElement -Tag div -Id 'DynamicTab1Content' -Content { Get-Date } 
    }
    New-UDTab -Text "Tab2" -Id 'DynamicTab2' -Dynamic -Content {
        New-UDElement -Tag div -Id 'DynamicTab2Content' -Content { Get-Date }
    }
    New-UDTab -Text "Tab3" -Id 'DynamicTab2' -Dynamic -Content {
        New-UDElement -Tag div -Id 'DynamicTab3Content' -Content { Get-Date }
    }
}

### EXAMPLE 3
```
Creates a vertical set of tabs.
```

New-UDTabs -Id 'verticalTabs' -Orientation 'vertical' -Tabs {
    New-UDTab -Text "Tab1" -Content {
        New-UDElement -Tag div -Content { Get-Date } 
    }
    New-UDTab -Text "Tab2" -Content {
        New-UDElement -Tag div -Content { Get-Date } 
    }
    New-UDTab -Text "Tab3" -Content {
        New-UDElement -Tag div -Content { Get-Date } 
    }
}

## PARAMETERS

### -Tabs
The tabs to put within this container.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id
The ID of the component.
It defaults to a random GUID.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: ([Guid]::NewGuid()).ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### -RenderOnActive
Whether to render the tabs when they are clicked.
Is this value isn't present, all the tabs are rendered, even if they are not shown.

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

### -Orientation
The orientation of the tabs.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: Horizontal
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
