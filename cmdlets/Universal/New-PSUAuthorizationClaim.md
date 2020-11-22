---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUAuthorizationClaim

## SYNOPSIS
Creates a new authorization claim. 

## SYNTAX

```
New-PSUAuthorizationClaim -Type <String> -Value <String> [-ValueType <String>] [-Properties <Hashtable>]
 [-Issuer <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new authorization claim. This cmdlet should be used within the Set-PSUAuthenticationMethod script block to assign claims to the user being authenticated.

## EXAMPLES

### Example 1
```powershell
Set-PSUAuthenticationMethod -ScriptBlock {
    param([PSCredential]$Credential)

    if ($Credential.UserName -eq 'admin')
    {
        New-PSUAuthenticationResult -Success -UserName 'admin' -Claims {
            New-PSUAuthorizationClaim -Type 'MyRole' -Value 'MyValue' -ValueType 'String' -Issuer 'Something'
        }
    }
    else 
    {
        New-PSUAuthenticationResult -ErrorMessage 'Hello'
    }
}

New-PSURole -Name 'CustomRole' -Policy {
    param($User)

    $User.HasClaim("MyRole", "MyValue")
}
```

Authenticates a user named 'admin' and adds a custom authorization claim. Authorization claims can be used in role policy scripts and are accessible in dashboards.

## PARAMETERS

### -Issuer
The issuer of the authorization claim.

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

### -Properties
A hashtable of properties to include with the claim.

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

### -Type
The type of claim.

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

### -Value
The value of the claim.

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

### -ValueType
The type of value for the claim.

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

[Set-PSUAuthenticationMethod](Set-PSUAuthenticationMethod.md)
[New-PSUAuthenticationResult](New-PSUAuthenticationResult.md)