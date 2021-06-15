---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUAccessControl

## SYNOPSIS
Defines advanced access controls for scripts.

## SYNTAX

### Tag
```
New-PSUAccessControl -Role <String> -Tag <String> -Type <AccessControlType> [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

### Object
```
New-PSUAccessControl -Role <String> -Type <AccessControlType> [-ObjectId <String>]
 -ObjectType <AccessControlObjectType> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [<CommonParameters>]
```

## DESCRIPTION
Defines advanced access controls for scripts.

## EXAMPLES

### Example 1
```powershell
$Type = ([PowerShellUniversal.AccessControlType]::Create -bor [PowerShellUniversal.AccessControlType]::View)
New-PSUAccessControl -Role 'ScriptBuilder' -ObjectType 'Script' -Type $Type
```

Global access controls allow you to define an access for a role for all resources of the chosen type. 
For example, to allow any user with the ScriptBuilder role to create a script, you can define an access control using the following command. You'll also want to grant the View privilege so that the user can also view scripts. 

### Example 2
```powershell
$Type = ([PowerShellUniversal.AccessControlType]::Execute -bor [PowerShellUniversal.AccessControlType]::View)
New-PSUAccessControl -Role 'ScriptRunner' -ObjectId 'OnBoarding.ps1' -ObjectType 'Script' -Type $Type
```

Resource access controls allow you to specify access controls directly on a resource. 
This example defines the execute privilege on the OnBoarding.ps1 script to the ScriptRunner role. 

### Example 3
```powershell
$Type = ([PowerShellUniversal.AccessControlType]::Edit -bor [PowerShellUniversal.AccessControlType]::View)
New-PSUAccessControl -Role 'ScriptEditor' -Tag 'HR' -Type $Type
```

$Type = ([PowerShellUniversal.AccessControlType]::Edit -bor [PowerShellUniversal.AccessControlType]::View)
New-PSUAccessControl -Role 'ScriptEditor' -Tag 'HR' -Type $Type


## PARAMETERS

### -AppToken
An app token used for accessing the management API.

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
The URI of the management API.

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

### -ObjectId
The ID of the object to set access controls for.

```yaml
Type: String
Parameter Sets: Object
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ObjectType
The type of object to set access controls for.

```yaml
Type: AccessControlObjectType
Parameter Sets: Object
Aliases:
Accepted values: Script

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Role
The role that is granted access with this access control.

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

### -Tag
The tag to assign access controls to.

```yaml
Type: String
Parameter Sets: Tag
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Type
The access control type to provide to the role.

```yaml
Type: AccessControlType
Parameter Sets: (All)
Aliases:
Accepted values: None, View, Edit, Create, Delete, Execute, All

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
