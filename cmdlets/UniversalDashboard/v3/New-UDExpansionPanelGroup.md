---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDExpansionPanelGroup

## SYNOPSIS
Creates a group of expansion panels.

## SYNTAX

```
New-UDExpansionPanelGroup [-Id <String>] [-Children] <ScriptBlock> [-Popout] [-Type <String>]
 [<CommonParameters>]
```

## DESCRIPTION
Creates a group of expansion panels.
Use New-UDExpansionPanel to create children for a group.

## EXAMPLES

### EXAMPLE 1
```
Creates an expansion panel group.
```

New-UDExpansionPanelGroup -Items {
    New-UDExpansionPanel -Title "Hello" -Id 'expTitle' -Content {}

    New-UDExpansionPanel -Title "Hello" -Id 'expContent' -Content {
        New-UDElement -Tag 'div' -id 'expContentDiv' -Content { "Hello" }
    }

    New-UDExpansionPanel -Title "Hello" -Id 'expEndpoint' -Endpoint {
        New-UDElement -Tag 'div' -id 'expEndpointDiv' -Content { "Hello" }
    }
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
Position: Named
Default value: ([Guid]::NewGuid())
Accept pipeline input: False
Accept wildcard characters: False
```

### -Children
Expansion panels to include in this group.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases: Content

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Popout
Creates a popout style expansion panel group.

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

### -Type
The type of expansion panel group.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: Expandable
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
