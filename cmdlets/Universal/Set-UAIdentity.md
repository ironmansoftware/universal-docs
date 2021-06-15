---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Set-UAIdentity

## SYNOPSIS
Sets properties of an identity.

## SYNTAX

### Id
```
Set-UAIdentity [-Id] <Int64> [-Name <String>] [-Role <Role>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [<CommonParameters>]
```

### Identity
```
Set-UAIdentity [-Identity] <Identity> [-Name <String>] [-Role <Role>] [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

## DESCRIPTION
Sets properties of an identity.

## EXAMPLES

### Example 1
```
PS C:\> Set-UAIdentity -Id 123 -Name 'Adam'
```

Sets Identity 123's name to 'Adam'

### Example 2
```
PS C:\> $Identity = Get-UAIdentity -Name 'Adam'
PS C:\> Set-UAIdentity -Identity $Identity -Name 'Lee'
```

Sets the Identity Adam to Lee.

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

### -Id
The ID of the identity.

```yaml
Type: Int64
Parameter Sets: Id
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Identity
An Identity object returned by Get-UAIdentity.

```yaml
Type: Identity
Parameter Sets: Identity
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Name
The name to set on the identity.

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

### -Role
The Role to set on the identity.
Use Get-UARole to retrieve built in roles.

```yaml
Type: Role
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

### UniversalAutomation.Identity
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
