---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDPaper

## SYNOPSIS
Creates a paper.

## SYNTAX

```
New-UDPaper [[-Id] <String>] [[-Children] <ScriptBlock>] [[-Width] <String>] [[-Height] <String>] [-Square]
 [[-Style] <Hashtable>] [[-Elevation] <Int32>] [<CommonParameters>]
```

## DESCRIPTION
Creates a paper.
Paper is used to highlight content within a page.

## EXAMPLES

### EXAMPLE 1
```
Creates paper with a heading, custom style and an elevation of 4.
```

New-UDPaper -Children {
    New-UDHeading -Text "hi" -Id 'hi'
} -Style @{
    backgroundColor = '#90caf9'
} -Id 'paperElevation' -Elevation 4

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
Default value: ([Guid]::NewGuid()).ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Children
The content of this paper element.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases: Content

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Width
The width of this paper.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: 500
Accept pipeline input: False
Accept wildcard characters: False
```

### -Height
The height of this paper.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: 500
Accept pipeline input: False
Accept wildcard characters: False
```

### -Square
Whether this paper is square.

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

### -Style
The CSS style to apply to this paper.

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

### -Elevation
The elevation of this paper.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: 6
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES
General notes

## RELATED LINKS
