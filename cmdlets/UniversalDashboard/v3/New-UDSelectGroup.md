---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDSelectGroup

## SYNOPSIS
Creates a new select group.

## SYNTAX

```
New-UDSelectGroup [-Option] <ScriptBlock> [-Name] <String> [<CommonParameters>]
```

## DESCRIPTION
Creates a new select group.
This cmdlet is to be used with New-UDSelect.
Pass the result of this cmdlet to the -Option parameter to create a new select group.

## EXAMPLES

### EXAMPLE 1
```
Creates a new select with two select groups.
```

New-UDSelect -Id 'selectGrouped' -Option {
    New-UDSelectGroup -Name "Category 1" -Option {
        New-UDSelectOption -Name "One" -Value 1
        New-UDSelectOption -Name "Two" -Value 2
        New-UDSelectOption -Name "Three" -Value 3
    }
    New-UDSelectGroup -Name "Category 2" -Option {
        New-UDSelectOption -Name "Four" -Value 4
        New-UDSelectOption -Name "Five" -Value 5
        New-UDSelectOption -Name "Six" -Value 6
    }
} -DefaultValue 2 -OnChange { Show-UDToast -Message $EventData }

## PARAMETERS

### -Option
Options to include in this group.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
The name of the group.
This will be displayed in the select.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
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
