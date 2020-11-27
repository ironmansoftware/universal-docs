---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDTypography

## SYNOPSIS
Creates typography.

## SYNTAX

### text (Default)
```
New-UDTypography [-Id <String>] [-Variant <String>] [[-Text] <String>] [-Style <Hashtable>]
 [-ClassName <String>] [-Align <String>] [-IsEndPoint] [-GutterBottom] [-NoWrap] [-Paragraph]
 [<CommonParameters>]
```

### endpoint
```
New-UDTypography [-Id <String>] [-Variant <String>] [-Content <ScriptBlock>] [-Style <Hashtable>]
 [-ClassName <String>] [-Align <String>] [-IsEndPoint] [-GutterBottom] [-NoWrap] [-Paragraph]
 [<CommonParameters>]
```

## DESCRIPTION
Creates typography.
Typography allows you to configure text within a dashboard.

## EXAMPLES

### EXAMPLE 1
```
New-UDTypography -Text 'Hello' -Paragraph
```

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

### -Variant
The type of text to display.

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

### -Text
The text to format.

```yaml
Type: String
Parameter Sets: text
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Content
The content to format.

```yaml
Type: ScriptBlock
Parameter Sets: endpoint
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Style
A set of CSS styles to apply to the typography.

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

### -ClassName
A CSS className to apply to the typography.

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

### -Align
How to align the typography.

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

### -IsEndPoint
{{ Fill IsEndPoint Description }}

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

### -GutterBottom
The gutter bottom.

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

### -NoWrap
Disables text wrapping.

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

### -Paragraph
Whether this typography is a paragraph.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
