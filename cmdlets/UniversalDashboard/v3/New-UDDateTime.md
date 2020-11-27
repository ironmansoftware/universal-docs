---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDDateTime

## SYNOPSIS
This date and time component is used for formatting dates and times using the user's browser settings.

## SYNTAX

### LocalizedFormat (Default)
```
New-UDDateTime [-Id <String>] [-InputObject] <String> [-LocalizedFormat <String>] [<CommonParameters>]
```

### Format
```
New-UDDateTime [-Id <String>] [-InputObject] <String> [-Format <String>] [<CommonParameters>]
```

## DESCRIPTION
This date and time component is used for formatting dates and times using the user's browser settings.
Since Universal Dashboard PowerShell scripts run within the server, the date and time settings of the user's system are not taken into account.
This component formats date and time within the client's browser to take into account their locale and time zone.

## EXAMPLES

### EXAMPLE 1
```
Formats a date and time using the format 'DD/MM/YYYY'
```

New-UDDateTime -InputObject (Get-Date) -Format 'DD/MM/YYYY'

## PARAMETERS

### -Id
The ID of this component.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: [Guid]::NewGuid()
Accept pipeline input: False
Accept wildcard characters: False
```

### -InputObject
The date and time object to format.

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

### -Format
The format of the date and time. 
This component uses Day.JS.
You can learn more about formatting options on their documentation: https://day.js.org/docs/en/display/format

```yaml
Type: String
Parameter Sets: Format
Aliases:

Required: False
Position: Named
Default value: DD/MM/YYYY
Accept pipeline input: False
Accept wildcard characters: False
```

### -LocalizedFormat
The localized format for the date and time.
Use this format if you would like to take the user's browser locale and time zone settings into account.

```yaml
Type: String
Parameter Sets: LocalizedFormat
Aliases:

Required: False
Position: Named
Default value: LLL
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
