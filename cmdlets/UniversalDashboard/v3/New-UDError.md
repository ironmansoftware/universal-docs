---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDError

## SYNOPSIS
Creates a new error card.

## SYNTAX

```
New-UDError [-Message] <String> [[-Title] <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new error card.

## EXAMPLES

### EXAMPLE 1
```
Displays the error 'Invalid data' on the page.
```

New-UDError -Message 'Invalid data'

## PARAMETERS

### -Message
The message to display.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Title
A title for the card.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
