---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDTextbox

## SYNOPSIS
Creates a textbox.

## SYNTAX

```
New-UDTextbox [[-Id] <String>] [[-Label] <String>] [[-Placeholder] <String>] [[-Value] <Object>]
 [[-Type] <String>] [-Disabled] [[-Icon] <Object>] [-Autofocus] [-Multiline] [[-Rows] <Int32>]
 [[-RowsMax] <Int32>] [-FullWidth] [[-Mask] <String[]>] [<CommonParameters>]
```

## DESCRIPTION
Creates a textbox.
Textboxes can be used by themselves or within a New-UDForm.

## EXAMPLES

### EXAMPLE 1
```
Creates a standard textbox.
```

New-UDTextbox -Label 'text' -Id 'txtLabel'

### EXAMPLE 2
```
Creates a password textbox.
```

New-UDTextbox -Label 'password' -Id 'txtPassword' -Type 'password'

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

### -Label
A label to show above this textbox.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Placeholder
A placeholder to place within the text box.

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

### -Value
The current value of the textbox.

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

### -Type
The type of textbox.
This can be values such as text, password or email.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 5
Default value: Text
Accept pipeline input: False
Accept wildcard characters: False
```

### -Disabled
Whether this textbox is disabled.

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

### -Icon
The icon to show next to the textbox.

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 6
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Autofocus
Whether to autofocus this textbox.

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

### -Multiline
{{ Fill Multiline Description }}

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

### -Rows
{{ Fill Rows Description }}

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: 7
Default value: 1
Accept pipeline input: False
Accept wildcard characters: False
```

### -RowsMax
{{ Fill RowsMax Description }}

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: 8
Default value: 9999
Accept pipeline input: False
Accept wildcard characters: False
```

### -FullWidth
{{ Fill FullWidth Description }}

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

### -Mask
{{ Fill Mask Description }}

```yaml
Type: String[]
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
