---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-UAVariable

## SYNOPSIS
Creates a new variable in UA.

## SYNTAX

### Value
```
New-UAVariable -Name <String> [-Value <String>] [-Type <String>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [<CommonParameters>]
```

### InputObject
```
New-UAVariable -Name <String> [-InputObject <Object>] [-Type <String>] [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

### Secret
```
New-UAVariable -Name <String> -Vault <String> [-Type <String>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [<CommonParameters>]
```

## DESCRIPTION
Creates a new variable in UA.
Variables are available in all scripts that run within UA.

## EXAMPLES

### Example 1
```
PS C:\> New-UAVariable -Name 'UserName' -Value 'Adam'
```

Creates a new variable in UA named \`UserName\`.
You can use the $UserName variable in all your scripts.

### Example 2
```
PS C:\> New-UAVariable -Name 'UserName' -Value 'Adam' -Vault "Vault"
```

Creates a new variable in the vault named \`Vault\`.
The variable's value is not stored in UA and will only be retrieved when running scripts.

## PARAMETERS

### -AppToken
An app token to access the UA API.

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
The HTTP address of the UA REST API server.

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

### -InputObject
{{ Fill InputObject Description }}

```yaml
Type: Object
Parameter Sets: InputObject
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
The name of the variable.
You can reference this in your scripts just as you would with other variables.

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

### -Type
The .NET type of object .

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

### -Value
The value of the variable.

```yaml
Type: String
Parameter Sets: Value
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Vault
The vault to store the variable within.

```yaml
Type: String
Parameter Sets: Secret
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
