---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDChip

## SYNOPSIS
Creates a new chip.

## SYNTAX

### Icon (Default)
```
New-UDChip [-Id <String>] [[-Label] <String>] [[-OnDelete] <Object>] [[-OnClick] <Object>] [[-Icon] <Object>]
 [[-Style] <Hashtable>] [[-Variant] <String>] [<CommonParameters>]
```

### Avatar
```
New-UDChip [-Id <String>] [[-Label] <String>] [[-OnDelete] <Object>] [[-OnClick] <Object>]
 [[-Style] <Hashtable>] [[-Variant] <String>] [[-Avatar] <String>] [[-AvatarType] <String>]
 [<CommonParameters>]
```

## DESCRIPTION
Creates a new chip.
Chips can be used to display tags or little bits of data.

## EXAMPLES

### EXAMPLE 1
```
Creates a clickable chip with a custom style and icon.
```

$Icon = New-UDIcon -Icon 'user' -Size sm -Style @{color = '#fff'}
New-UDChip -Label "Demo User" -Id "chipIcon" -Icon $Icon -OnClick {Show-UDToast -Message 'test'} -Clickable -Style @{backgroundColor = '#00838f'}

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

### -Label
The label for the chip.

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

### -OnDelete
A script block to call when the chip is deleted.

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 9
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnClick
A script block to call when the chip is clicked.

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 8
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Icon
An icon to show within the chip.

```yaml
Type: Object
Parameter Sets: Icon
Aliases:

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Style
CSS styles to apply to the chip.

```yaml
Type: Hashtable
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Variant
The theme variant to apply to the chip.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: Default
Accept pipeline input: False
Accept wildcard characters: False
```

### -Avatar
An avatar to show within the chip.

```yaml
Type: String
Parameter Sets: Avatar
Aliases:

Required: False
Position: 5
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -AvatarType
The type of avatar to show in the chip.

```yaml
Type: String
Parameter Sets: Avatar
Aliases:

Required: False
Position: 6
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
