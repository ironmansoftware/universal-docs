---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-PSUScript

## SYNOPSIS
Returns scripts defined within UA.

## SYNTAX

### All (Default)
```
Get-PSUScript [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-Integrated]
 [<CommonParameters>]
```

### Id
```
Get-PSUScript [-Id] <Int64> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### Identity
```
Get-PSUScript [-Identity] <Identity> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### Folder
```
Get-PSUScript [-Folder] <Folder> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### Name
```
Get-PSUScript [-Name] <String> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### ByTagObject
```
Get-PSUScript [-Tag <Tag>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-Integrated]
 [<CommonParameters>]
```

## DESCRIPTION
Returns scripts defined within UA.

## EXAMPLES

### Example 1
```
PS C:\> Get-UAScript
```

Returns all scripts defined within UA.

### Example 2
```
PS C:\> Get-UAScript -Id 12
```

Returns the script with ID 12.

### Example 3
```
PS C:\> $Identity = Get-UAIdentity -Name 'Adam'
PS C:\> Get-UAScript -Identity $Identity
```

Returns all scripts created or modified by the identity 'Adam'.

### Example 4
```
PS C:\> Get-UAScript -FolderId 12
```

Returns all scripts with the folder with ID 12.

### Example 4
```
PS C:\> Get-UAScript -Name 'Script1.ps1'
```

Returns script 'Script1.ps1'

### Example 5
```
PS C:\> $Tag = Get-UATag -Name 'Release'
PS C:\> Get-UAScript -Tag $Tag
```

Returns all scripts with the 'Release' tag.

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

### -Folder
{{ Fill Folder Description }}

```yaml
Type: Folder
Parameter Sets: Folder
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Id
The ID of the script to return.

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
Returns scripts based created or edited by this Identity.

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

### -Name
The name of the script to return.

```yaml
Type: String
Parameter Sets: Name
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Tag
Returns scripts based on this tag.
Use Get-UATag to retrieve tags.

```yaml
Type: Tag
Parameter Sets: ByTagObject
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
### System.Int64
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
