---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Set-PSUAuthenticationMethod

## SYNOPSIS
Sets the authentication method settings.

## SYNTAX

### Type (Default)
```
Set-PSUAuthenticationMethod [-ScriptBlock <ScriptBlock>] [-Type <AuthenticationMethodType>] [-Disabled]
 [-Configure <ScriptBlock>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### SAML2
```
Set-PSUAuthenticationMethod [-ScriptBlock <ScriptBlock>] [-Type <AuthenticationMethodType>] [-Disabled]
 -CallbackPath <String> [-MetadataAddress <String>] [-SigningKey <String>] -EntityId <String>
 [-IdentityProviderEntityId <String>] [-ServiceCertificate <String>] [-SingleSignOnServiceUrl <String>]
 [-Configure <ScriptBlock>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### OIDC
```
Set-PSUAuthenticationMethod [-ScriptBlock <ScriptBlock>] [-Type <AuthenticationMethodType>] [-Disabled]
 -CallbackPath <String> -ClientId <String> [-ClientSecret <String>] [-Resource <String>] [-Authority <String>]
 [-ResponseType <String>] [-SaveTokens <Boolean>] [-UseTokenLifetime <Boolean>] [-RequireMfa]
 [-GetClaimsFromUserInfoEndpoint <Boolean>] [-Scopes <String>] [-CorrelationCookieSameSite <String>]
 [-Configure <ScriptBlock>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### WSFed
```
Set-PSUAuthenticationMethod [-ScriptBlock <ScriptBlock>] [-Type <AuthenticationMethodType>] [-Disabled]
 -CallbackPath <String> [-UseTokenLifetime <Boolean>] [-CorrelationCookieSameSite <String>] -Wtrealm <String>
 -Wreply <String> -MetadataAddress <String> [-Configure <ScriptBlock>] [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
Sets the authentication method settings. 

Authentication settings are stored in .universal/authentication.ps1

You can also use this cmdlet with the PowerShell Universal Management API.

## EXAMPLES

### Example 1
```
PS C:\> Set-PSUAuthenticationMethod -ScriptBlock {
    param($Credential) 

    if ($Credential.UserName -eq 'Adam')
    {
        New-PSUAuthenticationResult -Success -UserName 'Adam'
    }
    else 
    {
        New-PSUAuthenticationResult -ErrorMessage 'Not Adam!'
    }

}
```

Forms authentication script blocks receive a single $Credential parameter that contains a PSCredential object. You need to return a New-PSUAuthenticationResult from the script block to grant and deny access. 

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

### -ScriptBlock
The script block to execute when a user is logging in. 

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Disabled
Whether forms authentication is disabled. 

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

### -Authority
The OpenID Connect authority URL. 

```yaml
Type: String
Parameter Sets: OIDC
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -CallbackPath
The callback path the authority will call after authentication. 

```yaml
Type: String
Parameter Sets: SAML2, OIDC, WSFed
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ClientId
The OpenID Connect Client ID to supply the authority with. 

```yaml
Type: String
Parameter Sets: OIDC
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ClientSecret
The OpenID Connect Client Secret to supply the authority with. 

```yaml
Type: String
Parameter Sets: OIDC
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Configure
Additional configuration script that can be run to update the authentication provider settings. See our online documentation for more information.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -CorrelationCookieSameSite
The CorrelationCookieSameSite setting to use for OpenID Conenct or WS-Federation authentication. 

```yaml
Type: String
Parameter Sets: OIDC, WSFed
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -EntityId
The entity ID for SAML2 authentication.

```yaml
Type: String
Parameter Sets: SAML2
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -GetClaimsFromUserInfoEndpoint
Whether to return additional claims information from the OpenID Connect authority. This setting is not supported by all authorities. 

```yaml
Type: Boolean
Parameter Sets: OIDC
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -IdentityProviderEntityId
The Idetity Provider Entity ID for SAML2 authentication. This is usually the URL to call for authentication. 

```yaml
Type: String
Parameter Sets: SAML2
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Integrated
Executes the command internally rather than using the Management API. Only works when running script from within PowerShell Universal. 

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

### -MetadataAddress
The SAML2 or WS-Federation metadata address. For SAML2, this should be specified if it is different than the Identity Provider Entity ID.  For WS-Federation, this setting is required. 

```yaml
Type: String
Parameter Sets: SAML2
Aliases: MetadataUrl

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

```yaml
Type: String
Parameter Sets: WSFed
Aliases: MetadataUrl

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Resource
A resource to grant a token for when authenticating with OpenID Connect. 

```yaml
Type: String
Parameter Sets: OIDC
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ResponseType
The OpenID Connect response type. This can be token or code.

```yaml
Type: String
Parameter Sets: OIDC
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SaveTokens
Whether to save the tokens within the OpenID Connect cookie. 

```yaml
Type: Boolean
Parameter Sets: OIDC
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Scopes
Scopes to request during OpenID Connect authentication.

```yaml
Type: String
Parameter Sets: OIDC
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ServiceCertificate
The service certificate to use when authenticating against the SAML2 Identity Provider.

```yaml
Type: String
Parameter Sets: SAML2
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Type
The Authentication Method Type.

```yaml
Type: AuthenticationMethodType
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseTokenLifetime
Whether to use the token lifetime as the cookie lifetime.

```yaml
Type: Boolean
Parameter Sets: OIDC, WSFed
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Wreply
The WS-Federation Wreply setting. 

```yaml
Type: String
Parameter Sets: WSFed
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Wtrealm
The WS-Federation Wrealm setting. 

```yaml
Type: String
Parameter Sets: WSFed
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -RequireMfa
Enforce the MFA requirement for OpenID Connect. 

```yaml
Type: SwitchParameter
Parameter Sets: OIDC
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SigningKey
A certificate signing key to use with SAML2. 

```yaml
Type: String
Parameter Sets: SAML2
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SingleSignOnServiceUrl
The single signon service URL for SAML2. 

```yaml
Type: String
Parameter Sets: SAML2
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

[New-PSUAuthenticationResult](New-PSUAuthenticationResult.md)