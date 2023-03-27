---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSURole

## SYNOPSIS

Defines a new role within PowerShell Universal.

## SYNTAX

### Policy
```
New-PSURole -Name <String> [-Description <String>] -Policy <ScriptBlock> [-Disabled] [-DefaultRoute <String>]
 [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

### Claim
```
New-PSURole -Name <String> [-Description <String>] -ClaimType <String> -ClaimValue <String> [-Disabled]
 [-DefaultRoute <String>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-Integrated]
 [<CommonParameters>]
```

## DESCRIPTION

Defines a new role within PowerShell Universal. Roles are used to define authorization within the PowerShell Universal platform. Roles can be assigned statically to an Identity or can be assigned by the -Policy script block. The policy script block receives a $User parameter that contains the identity information and claims that an identity has been granted during authentication. 

Policy script blocks need to return either $true or $false to determine whether this particular identity should be provided the role. 

Roles configurations are stored in .universal/roles.ps1

You can also use this cmdlet to create roles through the REST API.

## EXAMPLES

### Example 1
```
New-PSURole -Name 'Developers' -Policy {
    param($User)

    $User.Claims.HasClaim('myGroup')
}
```

Creates a new role with a policy defined that checks to see if the user's claim contains the 'myGroup' claim.

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

### -Description

The description of this role to show within the Admin Console.

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

### -Name

The name of this role. The name is used for both display and for assigning resources like APIs and dashboards.

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

### -Policy

The policy script block to execute when determining whether to assign this role. 

```yaml
Type: ScriptBlock
Parameter Sets: Policy
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

### -Integrated
Executes the command internally rather than using the Management API. Only works when running script from within PowerShell Universal. 

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

### -ClaimType
The claim type to map for this role. See Role to Claim mapping in our documentation. 

```yaml
Type: String
Parameter Sets: Claim
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ClaimValue
The claim value to map for this role. See Role to Claim mapping in our documentation. 

```yaml
Type: String
Parameter Sets: Claim
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Disabled
Whether the role is disabled. 

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

### -DefaultRoute
The default URL to forward users in this role to.

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
