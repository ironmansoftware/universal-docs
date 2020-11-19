---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Grant-PSUAppToken

## SYNOPSIS
{{ Fill in the Synopsis }}

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
{{ Fill in the Description }}

## EXAMPLES

### Example 1
```powershell
PS C:\> {{ Add example code here }}
```

{{ Add example description here }}

## PARAMETERS

### -AppToken
{{ Fill AppToken Description }}

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
{{ Fill Audience Description }}

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
{{ Fill ComputerName Description }}

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
{{ Fill Expiry Description }}

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
{{ Fill Identity Description }}

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
{{ Fill IdentityName Description }}

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
{{ Fill Issuer Description }}

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
{{ Fill Role Description }}

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
{{ Fill SigningKey Description }}

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
