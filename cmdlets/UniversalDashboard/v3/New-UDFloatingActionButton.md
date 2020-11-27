---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDFloatingActionButton

## SYNOPSIS
Creates a new floating action button.

## SYNTAX

```
New-UDFloatingActionButton [[-Id] <String>] [[-Icon] <Object>] [[-Size] <Object>] [[-OnClick] <Object>]
 [<CommonParameters>]
```

## DESCRIPTION
Creates a new floating action button.
Floating action buttons are good for actions that make sense for an entire page.
They can be pinned to the bottom of a page.

## EXAMPLES

### EXAMPLE 1
```
Creates a floating action button with a user icon and shows a toast when clicked.
```

New-UDFloatingActionButton -Icon user -OnClick {
    Show-UDToast -Message 'Hello'
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
Default value: ([Guid]::NewGuid())
Accept pipeline input: False
Accept wildcard characters: False
```

### -Icon
The icon to put within the floating action button.

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

### -Size
The size of the button.

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: Large
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnClick
A script block to execute when the floating action button is clicked.

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
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
