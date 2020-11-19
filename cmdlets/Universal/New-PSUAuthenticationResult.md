---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUAuthenticationResult

## SYNOPSIS

Returns an authentication result for forms authentication. 

## SYNTAX

```
New-PSUAuthenticationResult [-Claims <ScriptBlock>] [-Success] [-UserName <String>] [-ErrorMessage <String>]
 [<CommonParameters>]
```

## DESCRIPTION

Returns an authentication result for forms authentication. This allows you to return the user name, whether the authentication was successful, custom claims and an error message when the user attempts to login. 

## EXAMPLES

### Example 1
```powershell
param($Credential)

if ($Credential.UserName -eq 'Adam')
{
    New-PSUAuthenticationResult -UserName 'Adam' -Success
}
else 
{
    New-PSUAuthenticationResult -ErrorMessage "Hey! You aren't Adam"
}

```

Returns a successful authentication result if the user name is 'Adam'. Returns a custom error message if that user is not. 

## PARAMETERS

### -Claims

The claims to return from this authentication result. Claims typically are features of the current user account like the Active Directory group membership. Use the new-PSUAuthorizationClaim cmdlet to define these claims. 

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

### -ErrorMessage

The custom error message to return upon unsuccessful logins. 

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

### -Success

A switch parameter that signals that this authentication attempt was successful. 

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

### -UserName

The user name to set on the identity of the user logging in. 

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[New-PSUAuthorizationClaim](New-PSUAuthorizationClaim.md)
[Set-PSUAuthenticationMethod](Set-PSUAuthenticationMethod.md)