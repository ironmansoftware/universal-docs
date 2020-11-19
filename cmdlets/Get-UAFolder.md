---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-UAFolder

## SYNOPSIS
Returns folders defined within UA.

## SYNTAX

### All (Default)
```
Get-UAFolder [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### Children
```
Get-UAFolder [-Parent <Folder>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### Id
```
Get-UAFolder [-Id <Int64>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### Name
```
Get-UAFolder [-Name <String>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
Returns folders defined within UA.
Folders will be based on the internal and\or remote git repo.

## EXAMPLES

### Example 1
```
PS C:\> Get-UAFolder
```

Returns all folders within UA.

### Example 2
```
PS C:\> Get-UAFolder -Name 'Folder 1'
```

Returns the folder with the name 'Folder 1'

### Example 3
```
PS C:\> $Parent = Get-UAFolder -Name 'Parent'
PS C:\> Get-UAFolder -Parent $Parent
```

Returns all the children folders for the specified folder.

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
The ID of the folder to return.

```yaml
Type: Int64
Parameter Sets: Id
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
The name of the folder to return.

```yaml
Type: String
Parameter Sets: Name
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Parent
The parent folder to return children for.

```yaml
Type: Folder
Parameter Sets: Children
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
