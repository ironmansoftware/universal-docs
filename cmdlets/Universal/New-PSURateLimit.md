---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSURateLimit

## SYNOPSIS

Creates a new rate limit for the PowerShell Universal server.

## SYNTAX

```
New-PSURateLimit -Endpoint <String> -Period <TimeSpan> -Limit <Int32> [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

## DESCRIPTION

Creates a new rate limit for the PowerShell Universal server. Rate limits affect the entire server. You can limit the scope of the rate limit based on URLs. 

Rate limit configurations are stored in .universal/rateLimits.ps1

You can also use this cmdlet to create rate limits through the REST API.

You can use Set-PSUSetting to configure allow lists for IPs, endpoints and computer names that are not affected by the rate limiting.

## EXAMPLES

### Example 1
```powershell
New-PSURateLimit -Endpoint "/myEndpoint" -Period ([TimeSpan]::FromMinutes(10)) -Limit 100
```

Creates a new rate limit that prevents the user from calling the /myEndpoint endpoint more than 100 times in 10 minutes. 

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

The URL of the endpoint to rate limit. The URL can contain wildcards using the * character.

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

### -Limit

The number of requests over the period.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Period

The period of time to enforce the limit.

```yaml
Type: TimeSpan
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
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

### None

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[Set-PSUSetting](Set-PSUSetting.md)