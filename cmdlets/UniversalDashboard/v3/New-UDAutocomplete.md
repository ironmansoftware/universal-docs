---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDAutocomplete

## SYNOPSIS
Creates an autocomplete textbox.

## SYNTAX

### Dynamic
```
New-UDAutocomplete [-Id <String>] [-Label <String>] [-Value <String>] [-OnChange <Endpoint>]
 -OnLoadOptions <Endpoint> [<CommonParameters>]
```

### Static
```
New-UDAutocomplete [-Id <String>] [-Label <String>] [-Value <String>] [-OnChange <Endpoint>] -Options <Array>
 [<CommonParameters>]
```

## DESCRIPTION
Creates an autocomplete textbox.
Autocomplete text boxes can be used to allow the user to select from a large list of static or dynamic items.
Typing in the textbox will filter the list.

## EXAMPLES

### EXAMPLE 1
```
Creates a autocomplete with a static list of options.
```

New-UDAutocomplete -Id 'autoComplete' -Options @('Test', 'Test2', 'Test3', 'Test4')

### EXAMPLE 2
```
Creates an autocomplete with a dynamically filtered set of options
```

New-UDAutocomplete -Id 'autoCompleteDynamic' -OnLoadOptions { 
    @('Test', 'Test2', 'Test3', 'Test4') | Where-Object { $_ -match $Body } | ConvertTo-Json
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
Position: Named
Default value: ([Guid]::NewGuid())
Accept pipeline input: False
Accept wildcard characters: False
```

### -Label
The label to show for the textbox.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Value
The value of the textbox.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnChange
A script block that is invoked when the selection changes.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnLoadOptions
A script block that is called when the user starts typing in the text box.
The $Body variable will contain the typed text.
You should return a JSON array of values that are a result of what the user has typed.

```yaml
Type: Endpoint
Parameter Sets: Dynamic
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Options
Static options to display in the selection drop down.
When the user types, these options will be filtered.

```yaml
Type: Array
Parameter Sets: Static
Aliases:

Required: True
Position: Named
Default value: @()
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
