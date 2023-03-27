---
external help file: UniversalDashboard.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-UDHtml

## SYNOPSIS
Displays HTML on a dashboard. 

## SYNTAX

```
New-UDHtml [-Markup] <String> [<CommonParameters>]
```

## DESCRIPTION
Displays HTML on a dashboard. 

## EXAMPLES

### Example 1
```powershell
New-UDHTML -Markup "<blink>Hello!</blink>"
```

Creates blinking text on a page. 

## PARAMETERS

### -Markup
The HTML markup to display. 

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
