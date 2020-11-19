---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-PSUEndpoint

## SYNOPSIS
Returns all endpoints defined in PowerShell Universal. 

## SYNTAX

### All (Default)
```
Get-PSUEndpoint [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### Id
```
Get-PSUEndpoint [-Id <Int64>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### Url
```
Get-PSUEndpoint [-Url <String>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
Returns all endpoints defined in PowerShell Universal. 

## EXAMPLES

### Example 1
```
PS C:\> Get-PSUEndpoint
```

Returns all endpoints.

### Example 2
```
PS C:\> Get-PSUEndpoint -Id 1
```

Returns the endpoint that has Id 1. Ids are reset when the server is restarted. 

### Example 3
```
PS C:\> Get-PSUEndpoint -Url '/url'
```

Returns the endpoints that have the URL '/url'.

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
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id
The ID of the endpoint to return. 

```yaml
Type: Int64
Parameter Sets: Id
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Url
The URL of the endpoints to return. Multiple endpoints may have the same URL and different verbs. 

```yaml
Type: String
Parameter Sets: Url
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
