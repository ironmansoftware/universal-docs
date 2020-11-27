---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDCard

## SYNOPSIS
Creates a new card.

## SYNTAX

### Advanced
```
New-UDCard [-Id <String>] [-ClassName <String>] [-ShowToolBar] [-ToolBar <Object>] [-Header <Object>]
 [-Body <Object>] [-Expand <Object>] [-Footer <Object>] [-Style <Hashtable>] [-Elevation <Int32>]
 [<CommonParameters>]
```

### Text
```
New-UDCard [-Id <String>] [-ClassName <String>] [-ShowToolBar] [-Style <Hashtable>] [-Elevation <Int32>]
 [-Title <String>] [-TitleAlignment <String>] [-Text <String>] [<CommonParameters>]
```

### Simple
```
New-UDCard [-Id <String>] [-ClassName <String>] [-ShowToolBar] [-Style <Hashtable>] [-Elevation <Int32>]
 [-Title <String>] [-TitleAlignment <String>] [-Content <ScriptBlock>] [-Image <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new card.
Cards are used to display related content.

## EXAMPLES

### EXAMPLE 1
```
Shows a card with a title, image and content.
```

New-UDCard -Id 'SimpleCard' -Title "Alon" -Content { 
    "Content" 
} -Image 'https://avatars2.githubusercontent.com/u/34351424?s=460&v=4'

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
Default value: ([Guid]::NewGuid()).ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### -ClassName
A CSS class to assign to this card.

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

### -ShowToolBar
Whether to show the toolbar for this card.

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

### -ToolBar
The toolbar for this card.
Use New-UDCardToolbar to create a toolbar.

```yaml
Type: Object
Parameter Sets: Advanced
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Header
The header for this card.
The header typically contains a title for the card.
Use New-UDCardHeader to create a header.

```yaml
Type: Object
Parameter Sets: Advanced
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Body
The body for this card.
This is the main content for the card.
Use New-UDCardHeader to create a body.

```yaml
Type: Object
Parameter Sets: Advanced
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Expand
Th expand content for this card.
Expand content is show when the user clicks the expansion button.
Use New-UDCardExpand to create an expand.

```yaml
Type: Object
Parameter Sets: Advanced
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Footer
The footer for this card.
Footer contents typically contain actions that are relavent to the card.
Use New-UDCardFooter to create a footer.

```yaml
Type: Object
Parameter Sets: Advanced
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Style
Styles to apply to the card.

```yaml
Type: Hashtable
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Elevation
The amount of elevation to provide the card.
The more elevation, the more it will appear the card is floating off the page.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -Title
A title for the card.

```yaml
Type: String
Parameter Sets: Text, Simple
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -TitleAlignment
The alignment for the title.

```yaml
Type: String
Parameter Sets: Text, Simple
Aliases:

Required: False
Position: Named
Default value: Left
Accept pipeline input: False
Accept wildcard characters: False
```

### -Content
The content of the card.

```yaml
Type: ScriptBlock
Parameter Sets: Simple
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Image
An image to show in the card.

```yaml
Type: String
Parameter Sets: Simple
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Text
{{ Fill Text Description }}

```yaml
Type: String
Parameter Sets: Text
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
