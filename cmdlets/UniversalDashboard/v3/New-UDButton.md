---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDButton

## SYNOPSIS
Creates a new button.

## SYNTAX

```
New-UDButton [[-Text] <String>] [[-Icon] <Object>] [[-Variant] <String>] [[-IconAlignment] <String>]
 [-FullWidth] [[-OnClick] <Endpoint>] [[-Size] <String>] [[-Style] <Hashtable>] [[-Href] <String>]
 [-Id <String>] [-Color <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new button.
Buttons are used to allow the user to take action.

## EXAMPLES

### EXAMPLE 1
```
Creates a button with the GitHub logo and redirects the user to GitHub when clicked.
```

$Icon = New-UDIcon -Icon 'github'
New-UDButton -Text "Submit" -Id "btnClick" -Icon $Icon -OnClick {
    Invoke-UDRedirect https://github.com
}

## PARAMETERS

### -Text
The text to show within the button.

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

### -Icon
An icon to show within the button.
Use New-UDIcon to create an icon for this parameter.

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Variant
The variant type for this button.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: Contained
Accept pipeline input: False
Accept wildcard characters: False
```

### -IconAlignment
How to align the icon within the button.

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

### -FullWidth
Whether the button takes the full width of the it's container.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: 7
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnClick
The action to take when the button is clicked.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 8
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Size
The size of the button.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 9
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Style
Styles to apply to the button.

```yaml
Type: Hashtable
Parameter Sets: (All)
Aliases:

Required: False
Position: 10
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Href
A URL that the user should be redirected to when clicking the button.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 11
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
Position: Named
Default value: ([Guid]::NewGuid()).ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Color
{{ Fill Color Description }}

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: Default
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
