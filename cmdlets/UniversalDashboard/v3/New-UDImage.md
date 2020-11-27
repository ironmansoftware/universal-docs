---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDImage

## SYNOPSIS
An image component.

## SYNTAX

### url (Default)
```
New-UDImage [-Id <String>] [-Url <String>] [-Height <Int32>] [-Width <Int32>] [-Attributes <Hashtable>]
 [<CommonParameters>]
```

### path
```
New-UDImage [-Id <String>] [-Path <String>] [-Height <Int32>] [-Width <Int32>] [-Attributes <Hashtable>]
 [<CommonParameters>]
```

## DESCRIPTION
An image component.

## EXAMPLES

### EXAMPLE 1
```
Displays an image.
```

New-UDImage -Url 'https://ironmansoftware.com/logo.png'

## PARAMETERS

### -Id
The ID of this component.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: ([Guid]::NewGuid())
Accept pipeline input: False
Accept wildcard characters: False
```

### -Url
The URL to the image.

```yaml
Type: String
Parameter Sets: url
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
The path to a local image.

```yaml
Type: String
Parameter Sets: path
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Height
The height in pixels.

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

### -Width
The width in pixels.

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

### -Attributes
Additional attributes to apply to the img tag.

```yaml
Type: Hashtable
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: @{}
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
