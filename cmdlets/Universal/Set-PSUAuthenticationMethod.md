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

```
Set-PSUAuthenticationMethod -ScriptBlock <ScriptBlock> [-Disabled] [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

## DESCRIPTION
Sets the authentication method settings. This is currently only used to configure forms authentication. 

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

Required: True
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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[New-PSUAuthenticationResult](New-PSUAuthenticationResult.md)