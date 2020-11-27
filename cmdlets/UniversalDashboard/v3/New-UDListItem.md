---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDListItem

## SYNOPSIS
Creates a new list item.

## SYNTAX

```
New-UDListItem [[-Id] <String>] [[-AvatarType] <String>] [[-OnClick] <Endpoint>] [[-Label] <String>]
 [[-Children] <ScriptBlock>] [[-SubTitle] <String>] [[-Icon] <Object>] [[-Source] <String>]
 [[-SecondaryAction] <ScriptBlock>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new list item.
List items are used with New-UDList.

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

### -AvatarType
The type of avatar to show within the list item.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: Icon
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnClick
A script block to execute when the list item is clicked.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Label
The label to show within the list item.

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

### -Children
Nested list items to show underneath this list item.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases: Content

Required: False
Position: 5
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SubTitle
The subtitle to show within the list item.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 6
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Icon
The icon to show within the list item.

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 7
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Source
Parameter description

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 8
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SecondaryAction
The secondary action to issue with this list item.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: False
Position: 9
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
