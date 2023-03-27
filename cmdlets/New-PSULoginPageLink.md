---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSULoginPageLink

## SYNOPSIS
Creates a new link on the login page.

## SYNTAX

```
New-PSULoginPageLink -Text <String> -Url <String> [<CommonParameters>]
```

## DESCRIPTION
Creates a new link on the login page. Use in conjunction with New-PSULoginPage.

## EXAMPLES

### Example 1
```powershell
$LoginPage = @{
    Links = @(
        New-PSULoginPageLink -Text 'Google' -Url 'http://www.google.com'
        New-PSULoginPageLink -Text 'Microsoft' -Url 'http://www.microsoft.com'
    )
}

New-PSULoginPage @LoginPage
```

Creates a login page with two links.

## PARAMETERS

### -Text
The text of the link.

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

### -Url
The URL the link should go to.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
