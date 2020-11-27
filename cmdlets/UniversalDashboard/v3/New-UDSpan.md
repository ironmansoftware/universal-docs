---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDSpan

## SYNOPSIS
A span component.

## SYNTAX

```
New-UDSpan [[-Id] <String>] [[-Content] <Object>] [<CommonParameters>]
```

## DESCRIPTION
A span component.
Defines a span HTML tag.

## EXAMPLES

### EXAMPLE 1
```
An example
```

New-UDSpan -Content {
    New-UDTypography -Text 'Text'
}

## PARAMETERS

### -Id
The ID of this component.

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

### -Content
The content of the span.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
