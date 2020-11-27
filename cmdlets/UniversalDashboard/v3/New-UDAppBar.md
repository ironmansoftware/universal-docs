---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDAppBar

## SYNOPSIS
Creates an AppBar.

## SYNTAX

```
New-UDAppBar [[-Id] <String>] [[-Drawer] <Hashtable>] [[-Children] <ScriptBlock>] [[-Position] <String>]
 [<CommonParameters>]
```

## DESCRIPTION
Creates an AppBar.
This can be used to replace the built-in AppBar.

## EXAMPLES

### EXAMPLE 1
```
Creates a new AppBar that is relative to other components.
```

New-UDAppBar -Children { New-UDTypography -Text 'Hello' -Paragraph } -Position relative

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

### -Drawer
A drawer that can be opened from this AppBar.
Use New-UDDrawer to create a drawer to pass to this parameter.

```yaml
Type: Hashtable
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Children
Children of this AppBar.
The children of an AppBar are commonly text and buttons.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases: Content

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Position
The position of this AppBar.
A fixed position will override the default AppBar.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: Fixed
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
