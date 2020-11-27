---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDTimePicker

## SYNOPSIS
Creates a time picker.

## SYNTAX

```
New-UDTimePicker [[-Id] <String>] [[-Label] <String>] [[-OnChange] <Endpoint>] [[-Value] <String>]
 [<CommonParameters>]
```

## DESCRIPTION
Creates a time picker.
This component can be used stand alone or within New-UDForm.

## EXAMPLES

### EXAMPLE 1
```
Creates a new time picker
```

New-UDTimePicker -Id 'timePicker'

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
Default value: [Guid]::NewGuid().ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Label
The label to show with the time picker.

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

### -OnChange
A script block to call when the time is changed.
The $EventData variable contains the currently selected time.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Value
The current value of the time picker.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
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
