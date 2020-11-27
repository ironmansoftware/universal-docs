---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDList

## SYNOPSIS
Creates a list.

## SYNTAX

```
New-UDList [[-Id] <String>] [[-Children] <ScriptBlock>] [[-SubHeader] <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a list.
Use New-UDListItem to add new items to the list.
Lists are good for links in UDDrawers.

## EXAMPLES

### EXAMPLE 1
```
Creates a new list with two items and nested list items.
```

New-UDList -Id 'listContent' -Content {

    New-UDListItem -Id 'listContentItem' -AvatarType Avatar -Source 'https://pbs.twimg.com/profile_images/1065243723217416193/tg3XGcVR_400x400.jpg' -Label 'Adam Driscoll' -Content {

        New-UDListItem -Id 'list-item-security' -Label 'username and passwords'
        New-UDListItem -Id 'list-item-api' -Label 'api keys'

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
Position: 1
Default value: ([Guid]::NewGuid()).ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Children
The items in the list.

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

### -SubHeader
Text to show within the sub header.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
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
