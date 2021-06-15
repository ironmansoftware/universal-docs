---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Remove-PSUEndpoint

## SYNOPSIS

Deletes a PowerShell Universal endpoint

## SYNTAX

```
Remove-PSUEndpoint [-Endpoint] <Endpoint> [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [<CommonParameters>]
```

## DESCRIPTION
Deletes a PowerShell Universal endpoint

## EXAMPLES

### Example 1
```
PS C:\> Get-PSUEndpoint -Id 1 | Remove-PSUEndpoint
```

Removes the endpoint with Id 1. 

## PARAMETERS

### -AppToken
The AppToken that is used for calling the PowerShell Universal Management API. You can also call Connect-PSUServer before calling this cmdlet to set the AppToken for the entire session.

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

### -ComputerName
Specifies the computer name or URL that should be called when accessing the PowerShell Universal Management API. You can also use Connect-PSUServer before calling this cmdlet to set the computer name for the entire session. 

```yaml
Type: String
Parameter Sets: (All)
Aliases: Uri

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Endpoint
The endpoint to remove. Use Get-PSUEndpoint to retrieve endpoints. 

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -UseDefaultCredentials
Use default credentials when connecting to the management API

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

### UniversalAutomation.Endpoint
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[Get-PSUEndpoint](Get-PSUEndpoint.md)