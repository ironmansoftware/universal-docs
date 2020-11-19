---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Grant-PSUAppToken

## SYNOPSIS

Grants a new app token.

## SYNTAX

### GrantCustom (Default)
```
Grant-PSUAppToken -IdentityName <String> [-Expiry <DateTime>] [-Role <String>] [-ComputerName <String>]
 [-AppToken <String>] [<CommonParameters>]
```

### Grant
```
Grant-PSUAppToken -Identity <Identity> [-Expiry <DateTime>] [-Role <String>] [-ComputerName <String>]
 [-AppToken <String>] [<CommonParameters>]
```

### Generate
```
Grant-PSUAppToken -IdentityName <String> [-Expiry <DateTime>] [-Role <String>] [-Audience <String>]
 [-Issuer <String>] [-SigningKey <String>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
Grants a new app token. App tokens can be used to call the PowerShell Universal Management API and other custom REST APIs. 

## EXAMPLES

### Example 1
```powershell
PS C:\> Grant-PSUAppToken -IdentityName 'MyIdentity' -Expiry (Get-Date).AddDays(30) -Role 'Reader'
```

Grants a new app token to the MyIdentity user that expires in 30 days and provides Reader access.

### Example 2
```powershell
PS C:\> Grant-PSUAppToken -IdentityName 'MyIdentity' -Expiry (Get-Date).AddDays(30) -Role 'Reader' -SigningKey 'MySigningKey'
```

Generates a new app token using the specified signing key for the MyIdentity user.

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

### -Audience
The audience to use when generating a new app token. This needs to match the audience value on the server.

```yaml
Type: String
Parameter Sets: Generate
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

### -Expiry
The expiration date of the app token. 

```yaml
Type: DateTime
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Identity
The Identity object to create the app token for. Use Get-PSUIdentity to retrieve the identities.

```yaml
Type: Identity
Parameter Sets: Grant
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -IdentityName
The name of the identity to generate or grant for the app token. 

```yaml
Type: String
Parameter Sets: GrantCustom, Generate
Aliases: UserName, Application

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Issuer
The issue to set in the app token metadata. This needs to match the server's configuration settings.

```yaml
Type: String
Parameter Sets: Generate
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Role
The role to grant to the identity of the app token. 

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

### -SigningKey
The signing key used to sign the app token. This needs to match the server's configuration settings. 

```yaml
Type: String
Parameter Sets: Generate
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

[Get-PSUIdentity](Get-UAIdentity.md)