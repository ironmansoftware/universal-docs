---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDHeading

## SYNOPSIS
Defines a new heading

## SYNTAX

### Content
```
New-UDHeading [-Id <String>] [-Content <ScriptBlock>] [-Size <Object>] [-Color <DashboardColor>]
 [<CommonParameters>]
```

### Text
```
New-UDHeading [-Id <String>] [-Text <String>] [-Size <Object>] [-Color <DashboardColor>] [<CommonParameters>]
```

## DESCRIPTION
Defines a new heading.
This generates a new H tag.

## EXAMPLES

### EXAMPLE 1
```
A heading
```

New-UDHeading -Text 'Heading 1' -Size 1 -Color Blue

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

### -Content
The content of the heading.

```yaml
Type: ScriptBlock
Parameter Sets: Content
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Text
The text of the heading.

```yaml
Type: String
Parameter Sets: Text
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Size
This size of this heading.
This can be 1,2,3,4,5 or 6.

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Color
The text color.

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
