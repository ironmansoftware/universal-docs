---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-UARole

## SYNOPSIS
Returns the roles defined within UA.

## SYNTAX

### All (Default)
```
Get-UARole [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### Name
```
Get-UARole [[-Name] <String>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### Id
```
Get-UARole [[-Id] <Int64>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
Returns the roles defined within UA.
Roles specify what identities are capable of in UA.

## EXAMPLES

### Example 1
```
PS C:\> Get-UARole
```

Returns all roles defined within UA.

### Example 2
```
PS C:\> Get-UARole -Name 'Administrator'
```

Returns the Administrator role.

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
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id
The ID of the role to return.

```yaml
Type: Int64
Parameter Sets: Id
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
The name of the role to return.

```yaml
Type: String
Parameter Sets: Name
Aliases:

Required: False
Position: 0
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
