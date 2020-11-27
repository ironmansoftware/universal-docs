---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDParagraph

## SYNOPSIS
A paragraph.

## SYNTAX

### content
```
New-UDParagraph [-Content <ScriptBlock>] [-Color <DashboardColor>] [<CommonParameters>]
```

### text
```
New-UDParagraph [-Text <String>] [-Color <DashboardColor>] [<CommonParameters>]
```

## DESCRIPTION
A paragraph.
Used to define a P HTML tag.

## EXAMPLES

### EXAMPLE 1
```
A simple paragraph.
```

New-UDParagraph -Text 'Hello, world!'

## PARAMETERS

### -Content
The content of the paragraph.

```yaml
Type: ScriptBlock
Parameter Sets: content
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Text
The text of the paragraph.

```yaml
Type: String
Parameter Sets: text
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Color
The font color of the paragraph.

```yaml
Type: DashboardColor
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: Black
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
