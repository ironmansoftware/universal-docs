---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDCheckBox

## SYNOPSIS
Creates a checkbox.

## SYNTAX

```
New-UDCheckBox [[-Label] <String>] [[-Icon] <Object>] [[-CheckedIcon] <Object>] [[-OnChange] <Endpoint>]
 [[-Style] <Hashtable>] [-Disabled] [[-Checked] <Boolean>] [[-ClassName] <String>] [[-LabelPlacement] <String>]
 [[-Id] <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a checkbox.
Checkboxes can be used in forms or by themselves.

## EXAMPLES

### EXAMPLE 1
```
Creates a checkbox with a custom icon and style.
```

$Icon = New-UDIcon -Icon angry -Size lg  -Id 'demo-checkbox-icon' -Regular
$CheckedIcon = New-UDIcon -Icon angry -Size lg  -Id 'demo-checkbox-icon-checked' 
New-UDCheckBox -Id 'btnCustomIcon' -Icon $Icon -CheckedIcon $CheckedIcon -OnChange {} -Style @{color = '#2196f3'}

## PARAMETERS

### -Label
The label to show next to the checkbox.

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
The icon to show instead of the default icon.

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

### -CheckedIcon
The icon to show instead of the default checked icon.

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnChange
Called when the value of the checkbox changes.
The $EventData variable will have the current value of the checkbox.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Style
A hashtable of styles to apply to the checkbox.

```yaml
Type: Hashtable
Parameter Sets: (All)
Aliases:

Required: False
Position: 5
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Disabled
Whether the checkbox is disabled.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: 6
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Checked
Whether the checkbox is checked.

```yaml
Type: Boolean
Parameter Sets: (All)
Aliases:

Required: False
Position: 7
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -ClassName
A CSS class to assign to the checkbox.

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

### -LabelPlacement
Where to place the label.

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

### -Id
The ID of the component.
It defaults to a random GUID.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 9
Default value: ([Guid]::NewGuid()).ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
