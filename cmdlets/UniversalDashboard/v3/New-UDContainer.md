---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDContainer

## SYNOPSIS
Creates a Material UI container.

## SYNTAX

```
New-UDContainer [-Id <String>] [-Children] <ScriptBlock> [<CommonParameters>]
```

## DESCRIPTION
Creates a Material UI container.
Containers pad the left and right side of the contained content to center it on larger resolution screens.

## EXAMPLES

### EXAMPLE 1
```
Creates a container with some text.
```

New-UDContainer -Content {
    New-UDTypography -Text 'Nice'
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
Default value: ([Guid]::NewGuid()).ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Children
The child items to include within the container.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
