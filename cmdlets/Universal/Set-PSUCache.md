---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Set-PSUCache

## SYNOPSIS
Sets an object into the PowerShell Universal server-side cache.

## SYNTAX

### None (Default)
```
Set-PSUCache -Key <String> -Value <Object> [<CommonParameters>]
```

### Absolute
```
Set-PSUCache -Key <String> -Value <Object> [-AbsoluteExpiration <DateTime>] [<CommonParameters>]
```

### AbsoluteExpirationFromNow
```
Set-PSUCache -Key <String> -Value <Object> [-AbsoluteExpirationFromNow <TimeSpan>] [<CommonParameters>]
```

### Sliding
```
Set-PSUCache -Key <String> -Value <Object> [-SlidingExpiration <TimeSpan>] [<CommonParameters>]
```

## DESCRIPTION
Sets an object into the PowerShell Universal server-side cache. This cmdlet is to be used within APIs, Dashboards and Scripts. You cannot retrieve cache data from the Management API.

## EXAMPLES

### Example 1
```powershell
PS C:\> Set-PSUCache -Key 'Data' -Value 'MyValue'
```

Caches data forever within the server-level cache. 

### Example 2
```powershell
PS C:\> Set-PSUCache -Key 'Data' -Value 'MyValue' -AbsoluteExpirationTime (Get-Date).AddMinutes(10)
```

Caches data within the cache that will expire in 10 minutes. 

### Example 3
```powershell
PS C:\> Set-PSUCache -Key 'Data' -Value 'MyValue' -AbsoluteExpirationFromNow [TimeSpan]::FromMinutes(30)
```

Caches data within the cache that will expire in 30 minutes. 

### Example 4
```powershell
PS C:\> Set-PSUCache -Key 'Data' -Value 'MyValue' -SlidingExpiration [TimeSpan]::FromMinutes(10)
```

Caches data with a sliding cache of 10 minutes. If the data isn't accessed for 10 minutes, it will be invalidated and purged from the cache. If the data is accessed, the timer will reset for another 10 minutes. 

## PARAMETERS

### -AbsoluteExpiration
An absolute expiration time for the data in the cache. 

```yaml
Type: DateTime
Parameter Sets: Absolute
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -AbsoluteExpirationFromNow
A TimeSpan indicating how long from now the data should be removed from the cache. 

```yaml
Type: TimeSpan
Parameter Sets: AbsoluteExpirationFromNow
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Key
A key for looking up the data in the cache. 

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

### -SlidingExpiration
A TimeSpan indicating the sliding expiration for data in the cache. 

```yaml
Type: TimeSpan
Parameter Sets: Sliding
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Value
The object to store in the cache. This object will be serialized to CLIXML. 

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: True
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

[Get-PSUCache](Get-PSUCache.md)