---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDSwitch

## SYNOPSIS
Creates a new switch.

## SYNTAX

```
New-UDSwitch [[-Id] <String>] [-Disabled] [[-OnChange] <Endpoint>] [[-Checked] <Boolean>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new switch.
A switch behaves like a checkbox but looks a little different.

## EXAMPLES

### EXAMPLE 1
```
Creates a switch that shows a toast when changed.
```

New-UDSwitch -Id 'switchOnChange' -OnChange { 
    Show-UDToast -Message $EventData
}

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
Default value: ([Guid]::NewGuid())
Accept pipeline input: False
Accept wildcard characters: False
```

### -Disabled
Whether this switch is disabled.

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

### -OnChange
A script block that is called when this switch changes.
The $EventData variable will contain the checked value ($true\$false).

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Checked
Whether this switch is checked.

```yaml
Type: Boolean
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
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
