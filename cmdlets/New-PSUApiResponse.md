---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUApiResponse

## SYNOPSIS

Returns a custom API response from a PowerShell Universal REST API.

## SYNTAX

### Body (Default)
```
New-PSUApiResponse [-StatusCode <Int32>] [-Body <String>] [-Cookies <Hashtable>] [-ContentType <String>]
 [<CommonParameters>]
```

### Data
```
New-PSUApiResponse [-StatusCode <Int32>] [-Cookies <Hashtable>] [-Data <Byte[]>] [-ContentType <String>]
 [<CommonParameters>]
```

## DESCRIPTION

Returns a custom API response from a PowerShell Universal REST API. This cmdlet should be called within the -Endpoint script block defined in New-PSUEndpoint. 

## EXAMPLES

### Example 1
```powershell
New-PSUEndpoint -Url '/hello' -Method "GET" -Endpoint {
    New-PSUApiResponse -StatusCode 404 -Body "Not found!"
}
```

Returns a 404 status code from the /hello endpoint when the GET method is called. This is specifying a custom body as well. 

## PARAMETERS

### -Body

The body of the response to send back from the endpoint request. 

```yaml
Type: String
Parameter Sets: Body
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ContentType

The content-type header to set on the response from the endpoint.

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

### -Cookies

A hashtable of cookies to set in the HTTP response.

```yaml
Type: Hashtable
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Data

Binary data to return from the endpoint. This can be used to send binary files back to the user. 

```yaml
Type: Byte[]
Parameter Sets: Data
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -StatusCode

The HTTP status code to set for this response. The default value is 200.

```yaml
Type: Int32
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

[New-PSUEndpoint](New-PSUEndpoint)