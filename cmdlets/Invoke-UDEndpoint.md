---
external help file: UniversalDashboard.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Invoke-UDEndpoint

## SYNOPSIS
Invokes an endpoint directly.

## SYNTAX

```
Invoke-UDEndpoint -Id <String> [-Session] [-Wait] [<CommonParameters>]
```

## DESCRIPTION
Invokes an endpoint directly. For example, this can be used to execute button OnClick handlers.

## EXAMPLES

### Example 1
```powershell
New-UDButton -Text "Click Me" -OnClick {
    Show-UDToast "I was clicked!"
} -Id 'Button'

New-UDButton -Text "Invoke Me" -OnClick {
    Invoke-UDEndpoint -Id 'Button'
}
```

Click one button with another one. 

## PARAMETERS

### -Id
The ID of the endpoint to invoke. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Session
Whether to include user session information when invoke the endpoint. 

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Wait
Whether to wait for the endpoint to execute before continuing.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
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
