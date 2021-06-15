---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Set-UAVariable

## SYNOPSIS
Sets the properties of a variable.

## SYNTAX

### IdValue
```
Set-UAVariable [-Id] <Int64> [-Value <String>] [-Name <String>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [<CommonParameters>]
```

### IdInputObject
```
Set-UAVariable [-Id] <Int64> [-InputObject <Object>] [-Name <String>] [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

### VariableInputObject
```
Set-UAVariable [-Variable] <Variable> [-InputObject <Object>] [-Name <String>] [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

### VariableValue
```
Set-UAVariable [-Variable] <Variable> [-Value <String>] [-Name <String>] [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

## DESCRIPTION
Sets the properties of a variable.

## EXAMPLES

### Example 1
```
PS C:\> $Variable = Get-UAVariable -Name 'username'
PS C:\> Set-UAVariable -Variable $Variable -Value 'lee'
```

Sets the value of the username variable to lee.

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
The ID of the variable to set.

```yaml
Type: Int64
Parameter Sets: IdValue, IdInputObject
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -InputObject
{{ Fill InputObject Description }}

```yaml
Type: Object
Parameter Sets: IdInputObject, VariableInputObject
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
The name of the variable.

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
Parameter Sets: IdValue, VariableValue
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Variable
The variable to set.
Use Get-UAVariable to retrieve a Variable object.

```yaml
Type: Variable
Parameter Sets: VariableInputObject, VariableValue
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
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

### UniversalAutomation.Variable
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
